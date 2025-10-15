# MusicViewModel 功能总结

## 基本信息
- 包路径：`com.iven.musicplayergo`
- 父类：`AndroidViewModel`
- 用途：管理音乐播放器的音乐数据，处理音乐获取、过滤、分组及偏好设置更新等逻辑

## 协程管理
- 协程任务管理：通过`mViewModelJob`（`SupervisorJob`）管理所有协程，`onCleared()`和`cancel()`方法可取消该任务，终止所有相关协程
- 异常处理：`mHandler`（`CoroutineExceptionHandler`）处理协程异常，打印堆栈并将`deviceMusic`设为`null`
- 调度器：`mIoDispatcher`指定IO线程（结合`mViewModelJob`和`mHandler`），`mUiScope`指定主线程协程作用域

## 数据成员
- `deviceMusic`：`MutableLiveData<MutableList<Music>?>`，用于观察设备音乐列表变化
- `mDeviceMusicList`：存储设备上所有音乐的原始列表
- `deviceMusicFiltered`：过滤（去重、排除筛选条件）后的音乐列表
- 分组映射：
  - `deviceSongsByArtist`：按艺术家分组的音乐映射（key：艺术家，value：对应歌曲）
  - `deviceMusicByAlbum`：按专辑分组的音乐映射（key：专辑，value：对应歌曲）
  - `deviceMusicByFolder`：按文件夹分组的音乐映射（key：文件夹路径，value：对应歌曲）
  - `deviceAlbumsByArtist`：按艺术家分组的专辑映射（key：艺术家，value：对应专辑列表）

## 核心功能方法

### 音乐获取与查询
- `getDeviceMusic()`：启动协程，在IO线程获取音乐数据后，在主线程更新`deviceMusic`的`LiveData`值
- `queryForMusic(application: Application)`：通过`MediaStore`查询设备上的音乐文件，根据Android版本（Q及以上/以下）处理路径，解析音乐信息（艺术家、年份、标题等）并构建`Music`对象，添加到`mDeviceMusicList`
- `getMusic(application: Application)`：同步调用`startQuery`获取音乐，若列表非空则调用`buildLibrary`构建音乐库，返回`mDeviceMusicList`
- `startQuery(application: Application)`：调用`queryForMusic`并更新`mDeviceMusicList`

### 音乐库构建
- `buildLibrary(resources: Resources)`：
  - 去重：通过`distinctBy`根据艺术家、年份、轨道、标题、时长、专辑去重，生成`deviceMusicFiltered`
  - 过滤：根据偏好设置中的筛选条件，排除指定艺术家、专辑、路径的音乐
  - 分组：基于过滤后的列表，构建`deviceSongsByArtist`、`deviceMusicByAlbum`、`deviceMusicByFolder`分组映射
  - 专辑处理：为每个艺术家关联其专辑列表（通过`MusicUtils.buildSortedArtistAlbums`）

### 偏好设置更新
- `updatePreferences()`：更新偏好设置中的队列、收藏、最近播放歌曲等，确保与当前设备上的音乐一致：
  - 队列：更新歌曲ID和专辑ID，过滤设备上不存在的歌曲
  - 收藏：更新歌曲ID和专辑ID，过滤设备上不存在的歌曲
  - 队列起始歌曲：若不存在则替换为随机歌曲
  - 最近播放歌曲：若不存在则替换为队列首首歌曲（若队列存在）或随机歌曲

## 辅助方法
- `getSongFromIntent(queriedDisplayName: String)`：根据显示名从`mDeviceMusicList`中查找歌曲
- `getRandomMusic()`：从`deviceMusicFiltered`中返回随机歌曲
- `findMusic(song: Music?)`：根据标题、显示名、轨道、专辑、年份、时长从`deviceMusicFiltered`中查找匹配歌曲
