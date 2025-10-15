## RecyclerSheet.kt 功能说明

### 基本定位
- **类属性**：继承自 `BottomSheetDialogFragment`，是 Android 应用中的底部弹窗组件。
- **核心作用**：通过底部弹窗（BottomSheet）展示多种类型的列表内容（如主题设置、播放队列、收藏等），并处理用户交互。
- **依赖组件**：
  - ViewBinding（`ModalRvBinding`、`SleeptimerItemBinding`）：管理布局视图。
  - RecyclerView：展示列表数据，结合多种适配器（`AccentsAdapter`、`QueueAdapter` 等）。
  - 应用内模块：`GoPreferences`（偏好设置）、`MediaPlayerHolder`（媒体播放控制）、`UIControlInterface`（UI交互接口）等。


### 核心功能与类型
通过 `sheetType` 参数区分弹窗类型，每种类型对应不同列表内容和交互逻辑，主要类型包括：

1.** 主题颜色选择（ACCENT_TYPE）**- 功能：展示水平滚动的主题色列表（通过 `AccentsAdapter`），支持用户选择应用主题色。
   - 交互：选择后更新 `GoPreferences` 存储，并通过 `UIControlInterface` 通知 UI 刷新外观。

2.** 标签管理（TABS_TYPE）**- 功能：展示可拖拽排序的标签列表（通过 `ActiveTabsAdapter`），支持调整应用活跃标签页。
   - 交互：结合 `ItemTouchHelper` 实现拖拽排序，确认后更新偏好设置并刷新 UI。

3.** 过滤设置（FILTERS_TYPE）**- 功能：展示媒体过滤规则列表（通过 `FiltersAdapter`），管理过滤条件。
   - 交互：提供“清除过滤”按钮，确认后通过接口通知过滤规则更新。

4.** 播放队列（QUEUE_TYPE）**- 功能：展示当前播放队列歌曲（通过 `QueueAdapter`），支持滑动删除歌曲。
   - 交互：集成 `FastScroller` 快速滚动，支持清空队列，自动定位当前播放歌曲。

5.** 睡眠定时器（SLEEPTIMER_TYPE）**- 功能：展示定时关闭选项（如15分钟、30分钟，通过内部 `SleepTimerAdapter`）。
   - 交互：选择后设置 `MediaPlayerHolder` 的睡眠定时，到期自动暂停播放。

6.** 睡眠定时器倒计时（SLEEPTIMER_ELAPSED_TYPE）**- 功能：展示当前倒计时状态，提供“停止定时器”按钮。
   - 交互：点击按钮取消已设置的睡眠定时。

7.** 通知操作设置（NOTIFICATION_ACTIONS_TYPE）**- 功能：展示通知栏可配置操作列表（通过 `NotificationActionsAdapter`）。
   - 交互：调整通知栏功能，更新偏好设置。

8.** 收藏列表（FAV_TYPE）**- 功能：展示用户收藏歌曲（通过 `FavoritesAdapter`），支持滑动删除或添加到播放队列。
   - 交互：提供“清空收藏”按钮，支持批量/单个添加到队列。


### 关键交互与逻辑
-** 接口通信 **：通过 `UIControlInterface`（UI刷新）和 `MediaControlInterface`（媒体控制）与宿主 Activity 交互。
-** 状态回调 **：提供 `onQueueCancelled`、`onSleepTimerEnabled` 等回调，在弹窗关闭或状态变化时通知外部。
-** 列表交互 **：
  - 拖拽排序（标签管理）：通过 `ItemTouchHelper` 实现。
  - 滑动删除（队列、收藏）：结合适配器的滑动回调处理。
-** 偏好设置同步 **：用户操作（如主题色选择、过滤规则）实时更新到 `GoPreferences`，确保设置生效。


### 结构设计
-** 视图绑定 **：使用 `ModalRvBinding` 加载布局，避免 `findViewById`，提升性能。
-** 内部适配器 **：包含 `SleepTimerAdapter` 内部类，专门处理睡眠定时器选项的展示与选中逻辑。
-** 工厂方法 **：通过 `newInstance` 静态方法创建实例，通过 `which` 参数指定弹窗类型，符合 Fragment 最佳实践。


### 总结
`RecyclerSheet` 是一个高度复用的底部弹窗组件，通过类型参数适配多种列表场景（设置、播放控制、收藏管理等），统一了应用弹窗风格。通过接口和回调与外部模块低耦合通信，是音乐播放器中列表类交互的核心组件。
