# PlayerService.kt 功能解析

## 基本信息
- 类名：PlayerService
- 父类：Service（Android服务类，用于后台运行任务）
- 作用：音乐播放器的后台服务，负责音乐播放控制、媒体会话管理、通知管理、唤醒锁处理等核心功能

## 主要属性
1. **binder**: LocalBinder实例，用于客户端绑定服务时提供服务实例
2. **isRunning**: 标识服务是否正在运行
3. **mWakeLock**: PowerManager.WakeLock实例，用于保持设备唤醒状态（避免播放时休眠）
4. **mMediaPlayerHolder**: 媒体播放器持有者（单例），封装了实际的播放逻辑
5. **musicNotificationManager**: 音乐通知管理器，用于显示和更新播放通知
6. **isRestoredFromPause**: 标识是否从暂停状态恢复播放
7. **headsetClicks/ mLastTimeClick**: 用于处理耳机按键双击事件（双击切换下一曲）
8. **mMediaSessionCompat**: MediaSessionCompat实例，用于管理媒体会话（与系统媒体控制交互）
9. **mMediaSessionCallback**: 媒体会话回调，处理播放、暂停、切歌等命令

## 核心方法与功能

### 1. 媒体会话配置 (configureMediaSession)
- 初始化MediaSessionCompat，设置媒体按钮接收器和回调
- 关联媒体按钮广播接收器（MediaBtnReceiver），处理外部媒体控制事件
- 激活媒体会话，使其能够接收系统媒体控制命令

### 2. 服务生命周期方法
- **onCreate()**: 服务创建时调用，初始化唤醒锁（PARTIAL_WAKE_LOCK）
- **onStartCommand()**: 处理启动服务的意图（Intent），支持多种操作：
  - 收藏歌曲（FAVORITE_ACTION）
  - 快退/快进（REWIND_ACTION/ FAST_FORWARD_ACTION）
  - 上一曲/下一曲（PREV_ACTION/ NEXT_ACTION）
  - 播放/暂停（PLAY_PAUSE_ACTION）
  - 重复模式切换（REPEAT_ACTION）
  - 关闭服务（CLOSE_ACTION）
- **onDestroy()**: 服务销毁时调用，执行清理操作：
  - 保存播放状态（最后播放的歌曲、位置、队列等）到偏好设置
  - 释放媒体会话资源
  - 释放媒体播放器和唤醒锁
  - 更新运行状态标识

### 3. 绑定服务相关
- **onBind()**: 返回LocalBinder实例，允许客户端绑定服务并调用服务方法
- **LocalBinder**: 内部类，提供getService()方法获取PlayerService实例

### 4. 媒体按钮事件处理
- **handleMediaIntent()**: 处理媒体按钮事件（来自耳机或系统媒体控制）：
  - 播放/暂停（单击耳机按键）
  - 下一曲（双击耳机按键）
  - 上一曲/下一曲（对应媒体按键）
  - 停止播放（媒体停止按键）
  - 重新播放当前歌曲（媒体倒带按键）
- **MediaBtnReceiver**: 内部广播接收器，接收媒体按钮广播并转发给handleMediaIntent处理

### 5. 唤醒锁管理
- **acquireWakeLock()**: 获取唤醒锁（持续25秒），确保播放时设备不进入休眠
- **releaseWakeLock()**: 释放唤醒锁，节省电量

### 6. 通知管理
- **initializeNotificationManager()**: 初始化MusicNotificationManager，用于创建和更新播放通知
- 通知相关操作（如更新收藏图标）通过musicNotificationManager执行

## 关键常量
- **WAKELOCK_MILLI**: 唤醒锁持有时间（25000毫秒）
- **DOUBLE_CLICK**: 双击判定时间间隔（400毫秒）
