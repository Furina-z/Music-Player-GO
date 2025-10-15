# NotificationActionsAdapter 功能说明

## 基本作用
该类是一个 RecyclerView适配器，用于在音乐播放器应用的偏好设置中，展示和管理通知栏可使用的操作组合选项，允许用户选择通知栏中显示的操作按钮组合。

## 核心成员变量
- `selectedActions`：当前选中的通知操作组合，初始值从应用偏好设置（GoPreferences）中获取
- `mActions`：预设的通知操作组合列表，包含4种可选组合，每种组合是一个`NotificationAction`对象，包含两个操作（first和second）：
  - 第1项：(重复操作, 关闭操作)（默认选项）
  - 第2项：(倒回操作, 快进操作)
  - 第3项：(收藏操作, 关闭操作)
  - 第4项：(收藏位置操作, 关闭操作)

## 重写的 RecyclerView.Adapter方法
1. `onCreateViewHolder`：创建视图持有者，通过布局绑定（NotificationActionsItemBinding）加载item布局
2. `getItemCount`：返回可选项数量，即`mActions`列表的大小（4项）
3. `onBindViewHolder`：调用视图持有者的`bindItems`方法绑定数据到视图

## 内部类CheckableItemsHolder功能
负责单个item视图的绑定和事件处理，主要功能在`bindItems`方法中：
- 设置第一个操作按钮图标：通过`Theming.getNotificationActionIcon`获取对应图标资源
- 设置第二个操作按钮图标：同上，使用组合中的第二个操作
- 设置单选按钮状态：根据当前item是否为选中的操作组合（`selectedActions`）设置选中状态
- 设置item的内容描述：使用第一个操作的标题
- 点击事件处理：
  - 通知之前选中的item更新状态
  - 更新当前选中的操作组合（`selectedActions`）
  - 通知当前item更新状态
  - 将新选中的组合保存到应用偏好设置
- 长按事件处理：显示当前操作组合中第一个操作的标题提示（Toast）
