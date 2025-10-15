# MediaPlayerHolder.kt 功能说明

## 核心功能
- 封装MediaPlayer的核心功能，提供音乐播放、暂停、跳过、快进等控制接口
- 管理音频焦点，处理音频焦点获取、丢失及状态变化
- 维护播放状态（播放、暂停、恢复等）及相关元数据
- 处理音频效果（均衡器、低音增强、虚拟环绕声）
- 管理通知和前台服务，确保后台播放时的系统兼容性
- 处理外部事件（耳机插拔、蓝牙连接、媒体按钮等）

## 媒体播放控制
- 初始化媒体播放器：`initMediaPlayer()` 方法负责配置MediaPlayer，设置数据源、监听器和音频属性
- 播放/暂停控制：`resumeMediaPlayer()` 恢复播放，`pauseMediaPlayer()` 暂停播放，`resumeOrPause()` 切换播放状态
- 进度管理：通过 `startUpdatingCallbackWithPosition()` 和 `stopUpdatingCallbackWithPosition()` 维护播放进度更新
- 跳转控制：`skip()` 实现上一曲/下一曲切换，`fastSeek()` 实现快速进退，`seekTo()` 精确跳转至指定位置

## 音频焦点管理
- 音频焦点请求：`tryToGetAudioFocus()` 申请音频焦点，`initializeAudioFocusRequestCompat()` 配置音频焦点请求参数
- 焦点状态监听：`mOnAudioFocusChangeListener` 处理焦点变化（获取、丢失、暂时丢失等）
- 焦点状态处理：`configurePlayerState()` 根据当前焦点状态调整播放（暂停、降低音量、恢复播放等）

## 音频效果处理
- 均衡器相关：`initOrGetBuiltInEqualizer()` 初始化均衡器、低音增强和虚拟环绕声，`releaseBuiltInEqualizer()` 释放资源
- 效果配置：`restoreCustomEqSettings()` 恢复保存的均衡器设置，`setEqualizerEnabled()` 启用/禁用音频效果
- 系统均衡器：`openEqualizer()` 打开系统音频效果控制面板，`onSaveEqualizerSettings()` 保存自定义均衡器设置

## 播放队列与循环管理
- 队列控制：`manageQueue()` 处理队列播放，`setQueueEnabled()` 启用/禁用队列模式
- 循环模式：`repeat()` 切换循环模式（单曲循环、列表循环、关闭循环），通过 `isRepeat1X` 和 `isLooping` 标记状态

## 通知与前台服务
- 前台服务：`startForeground()` 启动前台服务并显示通知，处理Android 12+的ForegroundServiceStartNotAllowedException
- 通知更新：`mMusicNotificationManager` 管理通知内容更新，包括播放状态、封面、操作按钮等

## 其他功能
- 睡眠定时器：`pauseBySleepTimer()` 设置睡眠定时暂停，`cancelSleepTimer()` 取消定时
- 广播接收：`PlayerBroadcastReceiver` 接收处理耳机插拔、蓝牙连接、媒体按钮等广播事件
- 状态同步：`updatePlaybackStatus()` 更新媒体会话状态，`updateMediaSessionMetaData()` 同步媒体元数据至会话
