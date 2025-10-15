# MediaControlInterface 接口功能总结

该接口定义了媒体播放控制相关的回调方法，用于处理音乐播放过程中的各类操作，具体方法功能如下：

1. `onSongSelected(song: Music?, songs: List<Music>?, songLaunchedBy: String)`
   - 功能：处理歌曲被选中的操作
   - 参数：被选中的歌曲对象、当前歌曲列表、标识歌曲选中来源的字符串

2. `onSongsShuffled(songs: List<Music>?, songLaunchedBy: String)`
   - 功能：处理歌曲列表被打乱（随机播放）的操作
   - 参数：打乱后的歌曲列表、标识列表打乱来源的字符串

3. `onAddToQueue(song: Music?)`
   - 功能：处理将单首歌曲添加到播放队列的操作
   - 参数：要添加到队列的歌曲对象

4. `onAddAlbumToQueue(songs: List<Music>?, forcePlay: Pair<Boolean, Music?>)`
   - 功能：处理将专辑中的歌曲添加到播放队列的操作
   - 参数：专辑歌曲列表、包含是否强制播放（first）和需恢复歌曲（second）的Pair对象

5. `onUpdatePlayingAlbumSongs(songs: List<Music>?)`
   - 功能：处理正在播放的专辑歌曲列表更新的操作
   - 参数：更新后的专辑歌曲列表

6. `onPlaybackSpeedToggled()`
   - 功能：处理播放速度切换（如倍速播放切换）的操作

7. `onHandleCoverOptionsUpdate()`
   - 功能：处理封面相关选项更新（如封面显示设置变更）的操作

8. `onUpdatePositionFromNP(position: Int)`
   - 功能：处理从通知栏（NP）更新播放位置的操作
   - 参数：更新后的播放位置（整数）
