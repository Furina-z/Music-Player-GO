# Popups类功能总结

## 所属包
com.iven.musicplayergo.utils

## 主要功能
提供与音乐播放器相关的弹出菜单（PopupMenu）展示及交互处理功能。

## 核心方法

### 1. showPopupForSongs
- **参数**：
  - activity：当前活动（Activity）实例
  - itemView：弹出菜单依附的视图（View）
  - song：关联的音乐（Music）对象
  - launchedBy：标识菜单的启动来源
- **功能**：显示歌曲相关的弹出菜单
- **主要操作**：
  - 加载菜单资源R.menu.popup_songs
  - 设置菜单中歌曲标题为当前歌曲标题
  - 启用菜单图标
  - 设置菜单对齐方式为右对齐（Gravity.END）
  - 处理菜单项点击事件：
    - 点击"添加到收藏"（R.id.favorites_add）：调用Lists.addToFavorites添加歌曲到收藏，并通知UI更新收藏状态
    - 其他菜单项：调用MediaControlInterface的onAddToQueue方法将歌曲加入播放队列

### 2. showPopupForPlaybackSpeed
- **参数**：
  - activity：当前活动（Activity）实例
  - view：弹出菜单依附的视图（View）
- **功能**：显示播放速度选择的弹出菜单
- **主要操作**：
  - 加载菜单资源R.menu.popup_speed
  - 设置菜单对齐方式为右对齐（Gravity.END）
  - 当播放速度模式不是仅1.0倍速时，为当前选中的播放速度菜单项设置主题颜色
  - 处理菜单项点击事件：
    - 根据点击的菜单项ID确定对应的播放速度（0.25F到2.5F等）
    - 当播放速度模式不是仅1.0倍速时，为新选中的播放速度菜单项设置主题颜色
    - 调用MediaPlayerHolder.getInstance().setPlaybackSpeed设置播放速度

### 3. getSelectedPlaybackItem（私有方法）
- **参数**：playbackSpeed（播放速度，Float类型）
- **功能**：根据播放速度值返回对应的菜单项ID
- **映射关系**：
  - 0.25F → R.id.speed_0
  - 0.5F → R.id.speed_1
  - 0.75F → R.id.speed_2
  - 1.0F → R.id.speed_3
  - 1.25F → R.id.speed_4
  - 1.5F → R.id.speed_5
  - 1.75F → R.id.speed_6
  - 2.0F → R.id.speed_7
  - 2.25F → R.id.speed_8
  - 其他 → R.id.speed_9
