# TileService.kt 功能解析

这段代码定义了一个名为`PlayerTileService`的类，继承自Android的`TileService`，主要功能是实现快速设置面板中瓷砖的点击逻辑，具体说明如下：

### 1. 类声明与依赖：
   - 使用`@RequiresApi(Build.VERSION_CODES.N)`标注，表明该服务仅在Android N（API 24）及以上版本可用
   - 继承`TileService`，用于创建系统快速设置面板中的自定义瓷砖

### 2. 核心方法`onClick()`：
   - 该方法在用户点击快速设置中的对应瓷砖时触发
   - 内部创建一个指向`MainActivity`的意图（`Intent`）
   - 给意图添加额外参数`GoConstants.LAUNCHED_BY_TILE`，标识此次启动来自瓷砖点击
   - 设置意图标志：`FLAG_ACTIVITY_NEW_TASK`（在新任务中启动活动）和`FLAG_ACTIVITY_SINGLE_TOP`（若活动已在栈顶则不创建新实例）
   - 通过`startActivityAndCollapse(this)`启动`MainActivity`并折叠快速设置面板
