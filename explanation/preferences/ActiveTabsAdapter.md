# ActiveTabsAdapter 功能说明

## 基本功能
- 这是一个继承自 RecyclerView.Adapter的适配器类，用于管理和展示音乐播放器中的活跃标签页列表
- 负责处理标签项的显示、选中状态切换、交互逻辑等

## 核心变量
- `availableItems`：从偏好设置获取的可用标签列表（可变）
- `mActiveItems`：从偏好设置获取的当前活跃标签列表（可变）

## 主要方法
1. `getUpdatedItems()`：
   - 更新并返回可用标签列表
   - 确保保留活跃标签，同时尊重标签原有顺序

2. `onCreateViewHolder()`：
   - 创建视图持有者
   - 通过ActiveTabItemBinding加载列表项布局

3. `getItemCount()`：
   - 返回可用标签数量（即列表项数量）

4. `onBindViewHolder()`：
   - 绑定数据到视图持有者，调用`bindItems()`方法

## 内部类 CheckableItemsHolder
- 负责单个列表项的视图绑定和交互处理
- `bindItems()`方法：
  - 设置标签文本（通过`getTabText()`获取对应字符串资源）
  - 设置标签图标（通过Theming工具类获取）
  - 处理标签启用状态（设置标签不可点击/启用）
  - 调用`manageTabStatus()`管理标签选中状态样式
  - 处理点击事件：切换标签选中状态，更新`mActiveItems`，确保至少保留2个活跃标签

## 辅助方法
1. `manageTabStatus()`：
   - 管理标签选中/未选中状态的样式（颜色、图标状态等）
   - 根据选中状态设置图标、文本、拖拽手柄的颜色

2. `getTabText()`：
   - 根据标签类型（艺术家、专辑、歌曲、文件夹、设置）返回对应的字符串资源ID
