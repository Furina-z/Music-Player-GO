## 代码文件功能总结：GoConstants.kt

### 基本信息
- 所属包：`com.iven.musicplayergo`
- 类型：Kotlin对象（`object`），用于集中定义应用常量

### 1. 权限请求相关常量
- `PERMISSION_REQUEST_READ_EXTERNAL_STORAGE = 2588`：读取外部存储权限的请求码，用于权限请求回调识别

### 2. 启动与页面标识相关常量
- `LAUNCHED_BY_TILE`：标识应用是否通过快速tile（如桌面快捷方式）启动
- 标签页标识：`ARTISTS_TAB`、`ALBUM_TAB`、`SONGS_TAB`、`FOLDERS_TAB`、`SETTINGS_TAB`，分别对应艺术家、专辑、歌曲、文件夹、设置标签页
- `DEFAULT_ACTIVE_FRAGMENTS`：默认激活的标签页列表（包含上述所有标签页）
- 视图类型标识：`ARTIST_VIEW`（"0"）、`ALBUM_VIEW`（"1"）、`FOLDER_VIEW`（"2"），用于区分`MusicContainerListFragment`的实例化视图类型
- `RESTORE_FRAGMENT`：标识是否需要恢复碎片状态

### 3. 播放设置相关常量
- 播放速度：`PLAYBACK_SPEED_ONE_ONLY = "0"`（仅支持1倍速播放）
- 列表结束行为：`CONTINUE = "0"`（列表播放结束后的行为标识）
- 歌曲可视化：`FN = "1"`（歌曲可视化选项标识）

### 4. 排序方式相关常量
- 基础排序：`DEFAULT_SORTING`（0）、`ASCENDING_SORTING`（1，升序）、`DESCENDING_SORTING`（2，降序）
- 按轨道号排序：`TRACK_SORTING`（3）、`TRACK_SORTING_INVERTED`（4，反向）
- 按添加日期排序：`DATE_ADDED_SORTING`（5）、`DATE_ADDED_SORTING_INV`（6，反向）
- 按艺术家排序：`ARTIST_SORTING`（7）、`ARTIST_SORTING_INV`（8，反向）
- 按专辑排序：`ALBUM_SORTING`（9）、`ALBUM_SORTING_INV`（10，反向）

### 5. 错误标识相关常量
- `TAG_NO_PERMISSION`：无权限错误标签
- `TAG_NO_MUSIC`：无音乐文件错误标签
- `TAG_NO_MUSIC_INTENT`：无音乐意图错误标签
- `TAG_SD_NOT_READY`：SD卡未就绪错误标签

### 6. 碎片（Fragment）标签相关常量
- `DETAILS_FRAGMENT_TAG`：详情碎片的标签
- `ERROR_FRAGMENT_TAG`：错误提示碎片的标签

### 7. 播放器状态相关常量
- 复用`PlaybackStateCompat`的状态：`PLAYING`（播放中）、`PAUSED`（暂停）、`RESUMED`（初始未播放状态，对应`STATE_NONE`）

### 8. 通知相关常量
- 通知渠道ID：`NOTIFICATION_CHANNEL_ID`（播放服务通知）、`NOTIFICATION_CHANNEL_ERROR_ID`（错误通知）
- 通知ID：`NOTIFICATION_ID`（播放通知）、`NOTIFICATION_ERROR_ID`（错误通知）
- 通知意图请求码：`NOTIFICATION_INTENT_REQUEST_CODE = 100`
- 通知动作标识：`FAST_FORWARD_ACTION`、`PREV_ACTION`、`PLAY_PAUSE_ACTION`、`NEXT_ACTION`、`REWIND_ACTION`、`REPEAT_ACTION`、`CLOSE_ACTION`、`FAVORITE_ACTION`、`FAVORITE_POSITION_ACTION`（对应通知栏的各类操作按钮）
