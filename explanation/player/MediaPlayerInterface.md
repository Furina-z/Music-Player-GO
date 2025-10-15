# MediaPlayerInterface 接口功能说明

## 所属包
com.iven.musicplayergo.player

## 方法功能说明
1. `onPositionChanged(position: Int)`：当媒体播放位置发生改变时触发的回调，参数 `position` 表示当前播放位置
2. `onStateChanged()`：当媒体播放器的状态（如播放、暂停、停止等）发生改变时触发的回调
3. `onClose()`：当媒体播放器关闭时触发的回调
4. `onUpdateRepeatStatus()`：当重复播放状态更新时触发的回调
5. `onQueueEnabled()`：当播放队列启用时触发的回调
6. `onQueueStartedOrEnded(started: Boolean)`：当播放队列开始或结束时触发的回调，参数 `started` 为 `true` 表示队列开始，为 `false` 表示队列结束
7. `onBackupSong()`：当进行歌曲备份操作时触发的回调
8. `onUpdateSleepTimerCountdown(value: Long)`：当睡眠计时器的倒计时更新时触发的回调，参数 `value` 表示当前倒计时值（单位可能为毫秒）
9. `onStopSleepTimer()`：当睡眠计时器停止时触发的回调
10. `onUpdateFavorites()`：当收藏的歌曲列表更新时触发的回调
11. `onRepeat(toastMessage: Int)`：当执行重复播放操作时触发的回调，参数 `toastMessage` 可能为提示消息的资源ID
12. `onListEnded()`：当播放列表播放结束时触发的回调
