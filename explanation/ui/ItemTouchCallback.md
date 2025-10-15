# ItemTouchCallback 类功能说明

## 基本信息
- 类名：ItemTouchCallback<T>
- 继承：ItemTouchHelper.SimpleCallback
- 泛型参数：T（集合中元素的类型）
- 构造参数：
  - collection: MutableList<T>（需要处理移动的数据源集合）
  - isActiveTabs: Boolean（标识是否为"活跃标签"模式的标志）


## 核心方法功能

### 1. 重写 onMove 方法
- 功能：处理 RecyclerView中item的移动逻辑
- 逻辑：
  - 移动条件判断：`isActiveTabs && viewHolder.absoluteAdapterPosition != collection.size -1 || !isActiveTabs`
    - 当isActiveTabs为true时，不允许移动最后一个item
    - 当isActiveTabs为false时，允许所有item移动
  - 若满足移动条件，调用私有方法onItemMove处理实际移动操作
- 返回值：是否允许移动（布尔值）


### 2. 重写 onSwiped 方法
- 功能：处理item滑动事件
- 实现：空实现（当前不处理任何滑动操作）


### 3. 重写 isLongPressDragEnabled 方法
- 功能：设置是否支持长按拖动
- 返回值：true（支持长按触发拖动）


### 4. 私有方法 onItemMove
- 功能：执行item移动的具体逻辑
- 逻辑：
  - 再次校验移动条件（同onMove中的条件）
  - 根据fromPosition和toPosition的大小关系，通过Collections.swap交换集合中对应位置的元素
  - 通知RecyclerView适配器item位置发生变化（adapter?.notifyItemMoved）
- 返回值：固定返回true
