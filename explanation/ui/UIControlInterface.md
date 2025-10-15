# UIControlInterface接口功能总结

该接口位于`com.iven.musicplayergo.ui`包下，定义了一系列与UI控制相关的回调方法，主要用于处理音乐播放器界面中的各类交互和状态变化，具体功能如下：

- `onAppearanceChanged(isThemeChanged: Boolean)`：处理外观变化（如主题改变）的回调
- `onOpenNewDetailsFragment()`：打开新详情碎片的回调
- `onArtistOrFolderSelected(artistOrFolder: String, launchedBy: String)`：艺术家或文件夹被选中的回调
- `onFavoritesUpdated(clear: Boolean)`：收藏内容更新的回调（含是否清空的参数）
- `onFavoriteAddedOrRemoved()`：收藏添加或移除的回调
- `onCloseActivity()`：关闭活动（Activity）的回调
- `onAddToFilter(stringsToFilter: List<String>?)`：添加内容到过滤器的回调
- `onFiltersCleared()`：过滤器被清空的回调
- `onDenyPermission()`：权限被拒绝的回调
- `onOpenPlayingArtistAlbum()`：打开当前播放艺术家专辑的回调
- `onOpenEqualizer()`：打开均衡器的回调
- `onOpenSleepTimerDialog()`：打开睡眠定时器对话框的回调
- `onEnableEqualizer()`：启用均衡器的回调
- `onUpdateSortings()`：更新排序方式的回调
