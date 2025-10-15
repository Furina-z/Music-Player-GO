## MusicExts.kt 扩展函数集合说明

### 1. MediaPlayerHolder 扩展（播放队列与媒体控制）
- `startSongFromQueue(selectedSong: Music?)`：从播放队列启动指定歌曲  
  - 功能：查找歌曲在队列中的位置，更新当前播放歌曲，重置队列恢复标记，初始化媒体播放器并开始播放。
- `setCanRestoreQueue()`：设置队列可恢复标记  
  - 功能：当队列非空且未启动时，记录当前播放位置，标记队列可恢复并启用队列功能。
- `addSongsToNextQueuePosition(songsToQueue: List<Music>)`：添加歌曲到当前播放位置的下一位  
  - 功能：先通过`removeDuplicates()`按`id`和`albumId`去重，若队列已启动则插入到当前位置后，否则直接添加到队列。


### 2. 字符串与URI处理扩展
- `String?.toFilenameWithoutExtension()`：移除文件名扩展名  
  - 功能：使用正则表达式`"(?<=.)\\.[^.]+$"`匹配并删除扩展名（如"audio.mp3"→"audio"）。
- `Long.toContentUri(): Uri`：音乐ID转换为内容URI  
  - 功能：生成`MediaStore.Audio.Media`的URI（`content://media/external/audio/media/{id}`），用于访问媒体库音频。
- `Long.toAlbumArtURI(): Uri`：专辑ID转换为封面URI  
  - 功能：生成专辑封面的URI（`content://media/external/audio/albumart/{albumId}`），用于加载专辑封面。
- `Uri.toBitrate(context: Context): Pair<Int, Int>?`：获取音频采样率和比特率  
  - 功能：通过`MediaExtractor`解析URI对应的音频文件，返回采样率（Hz）和比特率（Kbps）的Pair，失败返回null。


### 3. 专辑封面加载扩展
- `Long.waitForCover(context: Context, onDone: (Bitmap?, Boolean) -> Unit)`：异步加载专辑封面  
  - 功能：基于用户设置（`isCovers`）决定是否加载，通过Coil库异步请求，成功回调返回Bitmap，失败返回错误标记。


### 4. 时间与日期格式化扩展
- `Long.toFormattedDuration(isAlbum: Boolean, isSeekBar: Boolean)`：格式化毫秒时长  
  - 功能：  
    - 时长<60分钟：返回"mm:ss"格式；  
    - 时长≥60分钟：`isSeekBar`为true时返回"hh:mm:ss"，否则返回"hh:mm"。
- `Int.toFormattedDate(): String`：格式化秒级时间戳为日期  
  - 功能：通过`SimpleDateFormat("dd MMM yyyy", Locale.getDefault())`转换为"日 月 年"格式（如"15 Oct 2025"）。


### 5. 音乐元数据处理扩展
- `Int.toFormattedTrack(): Int`：格式化轨道号  
  - 功能：轨道号≥1000时取后三位（如1002→2），否则直接返回。
- `Int.toFormattedYear(resources: Resources): String`：格式化年份  
  - 功能：非0值直接返回，0则返回资源文件中的"unknown_year"字符串。


### 6. 音乐列表与排序操作扩展
- `List<Music>.findIndex(song: Music?)`：查找歌曲在列表中的索引  
  - 功能：通过`id`和`albumId`匹配，返回索引（未找到则为`RecyclerView.NO_POSITION`）。
- `Music?.toName(): String?`：获取歌曲显示名称  
  - 功能：根据用户设置（`songsVisualization`），优先显示标题或去除扩展名的文件名。
- 排序相关函数：  
  - `String?.findSorting(launchedBy: String)`：根据条件查找排序方式（匹配偏好设置中的`albumOrFolder`、`launchedBy`等）。  
  - `Music.findSorting()`：基于当前歌曲属性查找排序配置。  
  - `Music.findRestoreSorting(launchedBy: String): Int`：根据视图类型（艺术家/文件夹等）返回恢复排序模式。  
  - `Music.findRestoreSongs(sorting: Int, musicViewModel: MusicViewModel)`：从ViewModel获取列表并按指定模式排序。
