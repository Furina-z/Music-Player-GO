# FiltersAdapter.kt 功能解释

## 基本信息
- 类名：FiltersAdapter
- 父类：RecyclerView.Adapter<FiltersAdapter.CheckableItemsHolder>
- 用途：用于RecyclerView的适配器，管理过滤项的显示和状态切换

## 成员变量
- mItemsToRemove：可变列表，存储用户选择要移除的过滤项
- mAvailableItems：从偏好设置(GoPreferences)中获取的过滤项列表，经过排序并转为可变列表

## 核心方法
1. getUpdatedItems()：
   - 功能：返回更新后的过滤项集合
   - 逻辑：从mAvailableItems中移除mItemsToRemove包含的所有项，然后转为Set返回

2. onCreateViewHolder()：
   - 功能：创建视图持有者
   - 逻辑：通过FilterItemBinding加载布局，实例化CheckableItemsHolder并返回

3. getItemCount()：
   - 功能：返回列表项数量
   - 逻辑：返回mAvailableItems的大小

4. onBindViewHolder()：
   - 功能：绑定数据到视图持有者
   - 逻辑：调用CheckableItemsHolder的bindItems方法，传入对应位置的过滤项

## 内部类 CheckableItemsHolder
- 作用：持有每个列表项的视图，处理视图绑定和事件监听

- bindItems(itemFilter: String?) 方法：
  - 功能：绑定过滤项数据到视图
  - 逻辑：
    - 设置标题文本为当前过滤项
    - 监听复选框(filter)状态变化：
      - 选中状态(b=true)：标题文本色设为主题的主要文本色，从mItemsToRemove中移除当前项
      - 未选中状态(b=false)：标题文本色设为普通控件色，将当前项添加到mItemsToRemove
    - 给整个列表项(root)设置点击事件：点击时切换复选框的选中状态
