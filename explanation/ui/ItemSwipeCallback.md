# ItemSwipeCallback 类功能说明


## 1. 基本信息
- 所在包：com.iven.musicplayergo.ui
- 继承类：ItemTouchHelper.SimpleCallback
- 支持滑动方向：左右滑动（ItemTouchHelper.RIGHT 或 ItemTouchHelper.LEFT），不支持上下移动（构造函数中第一个参数为0）


## 2. 构造参数
| 参数名              | 类型                                   | 说明                                     |
|---------------------|----------------------------------------|------------------------------------------|
| isQueueDialog       | Boolean                                | 标识是否为队列对话框场景                 |
| isFavoritesDialog   | Boolean                                | 标识是否为收藏对话框场景                 |
| onSwipedAction      | (RecyclerView.ViewHolder, Int) -> Unit | 滑动结束后的回调函数，接收滑动的ViewHolder和方向参数 |


## 3. 重写方法说明

### 3.1 onMove
- 功能：控制RecyclerView的item是否支持上下移动
- 实现：固定返回false，表明不支持item的上下移动操作


### 3.2 onSwiped
- 功能：处理item被滑动结束后的逻辑
- 实现：调用构造参数传入的onSwipedAction回调函数，将滑动的ViewHolder和方向传递出去，由外部处理具体业务逻辑


### 3.3 onChildDraw（滑动时的视觉效果绘制）
- 功能：在item滑动过程中绘制背景和图标，实现滑动时的视觉反馈
- 核心逻辑：
  1. 初始化：
     - 背景：使用ColorDrawable，颜色通过Theming.resolveWidgetsColorNormal(context)获取
     - 图标：根据滑动方向和场景（isQueueDialog、isFavoritesDialog）动态选择
     - 图标垂直边距：(item高度 - 图标高度) / 2，用于计算图标垂直居中位置

  2. 向右滑动（dX > 0）：
     - 背景绘制范围：item左侧到当前滑动距离dX处（itemView.left 至 dX.toInt()）
     - 图标选择：
       - 若isQueueDialog为true且isFavoritesDialog为false：使用R.drawable.ic_delete（删除图标）
       - 其他情况：使用R.drawable.ic_queue_add（添加到队列图标）
     - 图标绘制范围：左边界为item左侧 + 图标垂直边距，右边界为左边界 + 图标宽度，上下边界为item顶部/底部 + 图标垂直边距

  3. 向左滑动（dX < 0）：
     - 背景绘制范围：当前滑动距离dX处到item右侧（itemView.right + dX.toInt() 至 itemView.right）
     - 图标选择：
       - 若isQueueDialog为true或isFavoritesDialog为true：使用R.drawable.ic_delete（删除图标）
       - 其他情况：使用R.drawable.ic_favorite（收藏图标）
     - 图标绘制范围：右边界为item右侧 - 图标垂直边距，左边界为右边界 - 图标宽度，上下边界为item顶部/底部 + 图标垂直边距

  4. 绘制流程：
     - 绘制背景（colorDrawableBackground.draw(c)）
     - 保存画布状态（save()）
     - 根据滑动方向裁剪画布（仅显示滑动露出的区域）
     - 绘制图标（icon?.draw(c)）
     - 恢复画布状态（restore()）
     - 调用父类方法完成后续绘制（super.onChildDraw(...)）
