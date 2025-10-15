# MusicNotificationManager 类功能解析

## 所属包与依赖
- 包路径：`com.iven.musicplayergo.player`
- 依赖：依赖于`PlayerService`、`MediaPlayerHolder`、`GoPreferences`等类，用于音乐播放器的通知管理

## 主要功能
该类主要负责音乐播放器通知的创建、更新、取消等管理操作，包括播放控制通知和错误提示通知，适配不同Android版本的通知特性。

## 核心属性
- `mMediaPlayerHolder`：获取媒体播放器实例，用于获取播放状态、媒体元数据等
- `mNotificationBuilder`：通知构建器，用于构建通知内容和样式
- `mNotificationManagerCompat`：通知管理器，用于发送、更新和取消通知
- `mNotificationActions`：获取通知构建器中的动作列表
- `notificationActions`：从偏好设置中获取通知的自定义动作

## 主要方法解析

### 1. getPendingIntent(playerAction: String)
- 功能：根据传入的播放动作（如播放、暂停、上一曲等）创建指向`PlayerService`的PendingIntent
- 适配：根据Android版本设置不同的标志（Marshmallow及以上使用`FLAG_IMMUTABLE`）

### 2. createNotification(onCreated: (Notification) -> Unit)
- 功能：创建音乐播放通知的核心方法
- 步骤：
  - 初始化通知构建器，指定通知渠道ID
  - 为Android O及以上版本创建通知渠道
  - 创建打开主界面的PendingIntent（点击通知时跳转）
  - 配置通知基本属性（分类、优先级、静默、可见性等）
  - 添加通知动作按钮（自定义动作、上一曲、播放/暂停、下一曲、自定义动作）
  - 设置媒体样式，关联媒体会话，指定紧凑视图中显示的动作
  - 更新通知内容并触发回调返回构建的通知

### 3. updateNotification()
- 功能：更新通知状态
- 操作：更新通知的"正在进行"状态（根据播放状态），更新播放/暂停动作，通过通知管理器发送更新

### 4. cancelNotification()
- 功能：取消（移除）当前显示的音乐播放通知

### 5. onHandleNotificationUpdate(isAdditionalActionsChanged: Boolean)
- 功能：处理通知更新逻辑
- 区分：如果是额外动作变化，更新第一个和第五个动作按钮；否则更新通知内容后刷新通知

### 6. updateNotificationContent(onDone: (() -> Unit)? = null)
- 功能：更新通知中的媒体内容信息
- 内容：从媒体元数据中获取并设置歌曲标题、艺术家、专辑、专辑封面等信息，完成后触发回调

### 7. updatePlayPauseAction()
- 功能：更新通知中的播放/暂停动作按钮（根据当前播放状态切换图标）

### 8. updateRepeatIcon()、updateFavoriteIcon()
- 功能：分别更新通知中重复动作、收藏动作的图标

### 9. getNotificationAction(action: String)
- 功能：根据动作字符串获取对应的通知动作按钮
- 操作：通过主题工具获取动作图标，结合PendingIntent构建NotificationCompat.Action

### 10. createNotificationForError()
- 功能：创建错误提示通知（如文件系统权限错误）
- 配置：指定错误通知渠道，设置图标、标题、内容和样式，发送错误通知

### 11. createNotificationChannel(id: String)
- 功能：为Android O及以上版本创建通知渠道
- 配置：设置渠道名称、重要性、灯光、振动、徽章等属性，注册渠道到系统
