## FavoritesAdapter.kt 代码功能说明

### 1. 基本信息
- **所属包**：`com.iven.musicplayergo.dialogs`
- **功能定位**：基于Kotlin的RecyclerView适配器，用于音乐播放器应用中展示和管理用户收藏的音乐列表
- **继承关系**：继承自`RecyclerView.Adapter<FavoritesAdapter.FavoritesHolder>`

### 2. 核心变量与回调接口
- **数据存储**：
  - `mFavorites`：存储用户收藏的音乐列表，初始数据来源于`GoPreferences`（应用偏好设置）
  - 类型为`MutableList<Music>?`，支持动态修改

- **回调接口**：
  - `onFavoritesCleared`：收藏列表清空时触发的回调
  - `onFavoritesUpdate`：收藏列表更新时触发的回调
  - `onFavoriteQueued`：单个收藏歌曲加入播放队列时的回调
  - `onFavoritesQueued`：全部收藏歌曲加入播放队列时的回调（参数包含是否强制播放当前选中歌曲及对应歌曲对象）

### 3. RecyclerView适配器核心方法
- **onCreateViewHolder**：
  - 功能：创建视图持有者
  - 实现：通过`MusicItemBinding`加载列表项布局（`music_item.xml`）

- **getItemCount**：
  - 功能：返回收藏列表的大小，决定RecyclerView显示的列表项数量
  - 实现：返回`mFavorites?.size!!`

- **onBindViewHolder**：
  - 功能：将数据绑定到视图持有者，为每个列表项设置内容和交互事件
  - 实现：调用`holder.bindItems()`方法绑定对应位置的音乐数据

### 4. 视图持有者（FavoritesHolder）
- **类型**：内部类，继承自`RecyclerView.ViewHolder`
- **核心方法**：`bindItems(favorite: Music?)`
  - 功能：设置单个列表项的显示内容和交互事件
  - 显示内容：
    - 歌曲标题（通过`toName()`方法处理）
    - 歌曲时长（通过`Dialogs.computeDurationText()`计算）
    - 艺术家和专辑信息（通过字符串格式化组合）
  - 交互事件：
    - 点击事件：触发`onFavoritesQueued`回调，将全部收藏歌曲加入队列并强制播放当前点击的歌曲
    - 长按事件：调用`showPopupForFavoriteSongs()`方法显示操作弹出菜单

### 5. 交互功能实现
- **弹出菜单（showPopupForFavoriteSongs）**：
  - 触发时机：长按列表项时
  - 菜单资源：`R.menu.popup_favorites_songs`
  - 功能：
    - 显示歌曲标题和操作选项（删除收藏、加入队列）
    - 支持显示图标，菜单位置居右
    - 点击"删除收藏"触发`performFavoriteDeletion`方法
    - 点击"加入队列"触发`onFavoriteQueued`回调

- **收藏删除功能（performFavoriteDeletion）**：
  - 功能：从收藏列表中删除指定歌曲并更新数据
  - 流程：
    1. 若应用设置了"删除前询问"（`isAskForRemoval`），则显示确认对话框
    2. 确认后调用`deleteSong()`方法执行删除操作：
       - 从`mFavorites`列表中移除歌曲
       - 调用`notifyItemRemoved`刷新列表
       - 更新`GoPreferences`中的收藏数据
       - 若列表为空，触发`onFavoritesCleared`回调
       - 触发`onFavoritesUpdate`回调通知列表更新

### 6. 总结
该适配器是音乐播放器中"收藏歌曲列表"的核心组件，负责：
- 收藏音乐的数据展示（标题、时长、艺术家、专辑）
- 用户交互处理（点击播放、长按操作菜单）
- 收藏管理（删除、列表更新、偏好设置同步）
- 通过回调机制与外部组件（播放控制、偏好设置）解耦通信
