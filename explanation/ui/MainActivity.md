# MainActivity.kt 功能总结

## 基础信息
- 类定义：`class MainActivity : BaseActivity(), UIControlInterface, MediaControlInterface`
- 作用：音乐播放器应用的主活动，统筹管理界面与媒体控制逻辑

## 核心成员变量
- 视图绑定：`mMainActivityBinding`、`mPlayerControlsPanelBinding`
- 数据与配置：`mMusicViewModel`（音乐数据）、`mGoPreferences`（偏好设置）
- 碎片管理：`mArtistsFragment`、`mAllMusicFragment`等多种功能碎片实例
- 媒体相关：`mMediaPlayerHolder`（播放器核心）、`mPlayerService`（播放服务）、`sBound`（服务绑定状态）
- 对话框：`mQueueDialog`（队列）、`mNpDialog`（正在播放）等

## 服务交互
- 服务绑定：通过`ServiceConnection`实现与`PlayerService`的绑定，在`onServiceConnected`中初始化播放器并加载音乐数据
- 绑定/解绑：`doBindService()`绑定服务，`onDestroy`中根据播放状态解绑并停止服务

## 生命周期管理
- `onCreate`：初始化主题、方向、视图绑定，设置返回键回调
- `onStart`：检查存储权限，权限通过则绑定服务
- `onResume`/`onPause`：处理播放进度回调的启停
- `onDestroy`：清理资源，停止服务（非播放状态下）

## 界面初始化
- 视图页管理：`initViewPager()`初始化`ViewPager2`，`ScreenSlidePagerAdapter`管理碎片切换
- 标签栏：`initTabLayout()`关联`TabLayout`与`ViewPager2`，处理标签选择事件
- 错误处理：`notifyError()`显示错误碎片（无权限/无音乐等场景）

## 媒体控制功能
- 播放控制：`playPauseButton`点击触发`mMediaPlayerHolder.resumeOrPause()`
- 队列管理：`queueButton`点击打开队列对话框，长按清空队列
- 收藏管理：`favoritesButton`点击打开收藏列表，长按清空收藏
- 详情页：`openDetailsFragment()`打开，`closeDetailsFragment()`关闭，支持动画效果
- 其他功能：均衡器调用（`onOpenEqualizer()`）、睡眠定时器（`onOpenSleepTimerDialog()`）、播放速度切换等

## 事件处理
- 返回键：`handleBackPressed()`处理（关闭详情页/切换标签/退出应用）
- 权限请求：`onRequestPermissionsResult()`处理存储权限结果
- 意图处理：`onNewIntent()`处理外部启动意图（如快捷方式）

## 状态恢复与更新
- `restorePlayerStatus()`：恢复上次播放状态（从偏好设置读取最近播放歌曲）
- `updatePlayingInfo()`：更新播放信息（歌曲名、艺术家、进度条等）
- `onFavoritesUpdated()`：更新收藏状态及UI显示
