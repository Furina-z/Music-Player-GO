## DetailsFragment 功能说明

### 基本概述
- 是一个继承自 Fragment 的子类，用于展示音乐相关的详细信息（艺术家、专辑、文件夹中的歌曲等）
- 实现 SearchView.OnQueryTextListener 接口，支持搜索功能
- 通过 ViewModel 获取音乐数据，与 Activity 通过接口交互（UIControlInterface、MediaControlInterface）

### 核心变量与状态
- `mLaunchedBy`：标识当前视图来源（艺术家视图、文件夹视图、专辑视图），对应常量：`GoConstants.ARTIST_VIEW`、`GoConstants.FOLDER_VIEW`、`GoConstants.ALBUM_VIEW`
- `mSelectedArtistOrFolder`：当前选中的艺术家或文件夹名称
- `mSelectedArtistAlbums`：当前艺术家的专辑列表
- `mSongsList`：当前展示的歌曲列表
- `mSongsSorting`：歌曲排序方式，通过 `Lists` 工具类处理不同排序逻辑

### 生命周期与初始化
- `onAttach`：获取传递的参数（选中的艺术家/文件夹、来源视图、选中的专辑位置等），初始化交互接口
- `onCreateView`：根据视图来源和设备方向（横屏）加载不同布局
- `onViewCreated`：观察 ViewModel 中的音乐数据，初始化工具栏和视图

### 视图与布局
- 支持不同视图模式的布局适配（艺术家、文件夹、专辑视图）
- 包含 RecyclerView 用于展示专辑列表（`albumsRv`）和歌曲列表（`songsRv`）
- 工具栏（`detailsToolbar`）：显示标题、副标题，包含菜单（排序、shuffle、添加到队列等）
- 专辑封面与信息展示区域：在专辑视图中显示专辑封面、标题、艺术家、歌曲数量等

### 核心功能

#### 1. 数据展示与更新
- 通过 `getSongSource` 方法根据视图来源获取对应的歌曲列表（艺术家的歌曲、文件夹的歌曲、专辑的歌曲）
- `setSongsDataSource` 方法处理歌曲数据的排序和适配器更新
- 支持根据排序方式（默认、升序、降序、按轨道、按日期等）刷新列表

#### 2. 交互功能
- 歌曲点击：触发播放选中歌曲，通过 `mMediaControlInterface.onSongSelected` 与播放器交互
- 歌曲长按：显示歌曲操作弹窗（`Popups.showPopupForSongs`）
- 滑动操作：通过 `ItemTouchHelper` 实现右滑添加到队列、左滑添加到收藏
- 专辑点击：在艺术家视图中切换选中的专辑，更新展示的歌曲列表

#### 3. 搜索功能
- 实现 `onQueryTextChange` 方法，实时根据搜索内容过滤歌曲列表
- 搜索时隐藏部分菜单选项，调整专辑封面显示状态

#### 4. 排序功能
- 工具栏菜单提供多种排序选项（默认、升序、降序、轨道顺序等）
- 通过 `applySortingToMusic` 方法应用排序，并保存用户排序偏好
- 排序图标根据当前排序方式动态更新

#### 5. 动画效果
- 视图创建和销毁时使用圆形揭露动画（`createCircularReveal`）
- 专辑封面和搜索框的滑动动画（`slide` 方法）

#### 6. 适配器
- `AlbumsAdapter`：展示专辑列表，处理专辑点击切换逻辑，显示专辑封面、标题、年份和总时长
- `SongsAdapter`：展示歌曲列表，显示歌曲标题（根据设置显示文件名或轨道+标题）、时长等信息，处理歌曲点击和长按事件

### 接口与回调
- `UIControlInterface`：与 Activity 交互处理 UI 相关操作（如打开睡眠定时器对话框、更新收藏状态）
- `MediaControlInterface`：与播放器交互（如播放选中歌曲、添加到队列、shuffle 播放）

### 其他功能
- 睡眠定时器：支持在菜单中打开睡眠定时器对话框，图标根据状态变色
- 状态保存与恢复：通过参数传递保存选中的歌曲ID、专辑位置等状态
- 适配深色模式：使用 `Theming` 工具类获取主题相关颜色和资源
