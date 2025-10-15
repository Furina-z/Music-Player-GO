## 总结：QueueAdapter.kt 功能概述

`QueueAdapter.kt` 是音乐播放器应用中负责管理播放队列展示与交互的 RecyclerView适配器，核心功能如下：

### 1. 基础定位
- 继承自 `RecyclerView.Adapter<QueueAdapter.QueueHolder>`，用于为播放队列的RecyclerView提供数据适配。
- 所属包为 `com.iven.musicplayergo.dialogs`，是对话框组件中展示播放队列的核心组件。


### 2. 核心依赖与数据关联
- 依赖 `MediaPlayerHolder` 单例：获取当前播放队列（`queueSongs`）、当前播放歌曲（`mSelectedSong`）等状态，实现播放控制联动。
- 依赖 `GoPreferences`：读取应用偏好设置（如删除前是否询问），规范交互逻辑。
- 数据核心：通过 `queueSongs` 存储播放队列中的歌曲列表（`List<Music>`），动态展示队列内容。


### 3. 核心功能与交互
- **队列展示**：通过 `QueueHolder` 绑定每首歌曲的标题、时长、艺术家+专辑信息，清晰呈现队列内容。
- **状态高亮**：通过 `isCurrentIndex` 判断并高亮显示当前正在播放的歌曲，直观区分播放状态。
- **播放切换**：点击队列中的歌曲时，通过 `MediaPlayerHolder` 直接切换播放该歌曲，实现快速选曲。
- **歌曲删除**：支持从队列中删除歌曲，通过 `performQueueSongDeletion` 处理：
  - 依据偏好设置决定是否显示删除确认对话框；
  - 禁止删除当前正在播放的歌曲；
  - 队列为空时触发 `onQueueCleared` 回调，通知外部处理空队列逻辑。


### 4. 整体作用
作为播放队列与UI之间的桥梁，该适配器实现了队列数据的动态展示、播放状态的直观反馈及用户交互（切换播放、删除歌曲）的处理，同时通过与媒体播放核心（`MediaPlayerHolder`）和偏好设置的联动，确保队列状态与播放逻辑的一致性。
