# AllMusicFragment 功能解析

## 基本信息
- 类名：AllMusicFragment
- 类型：Android Fragment子类
- 作用：展示设备上的所有音乐列表，提供音乐播放、搜索、排序等功能

## 核心依赖与接口
- 依赖：ViewModel（MusicViewModel）、MediaPlayerHolder、GoPreferences等
- 实现接口：SearchView.OnQueryTextListener（处理搜索功能）
- 回调接口：UIControlInterface（UI控制）、MediaControlInterface（媒体控制）

## 生命周期方法
1. **onAttach**：绑定上下文，获取回调接口实例
2. **onDestroyView**：释放视图绑定实例
3. **onCreateView**：初始化视图绑定
4. **onViewCreated**：初始化ViewModel，观察设备音乐数据变化

## 核心功能

### 1. 音乐数据处理
- 通过MusicViewModel观察设备音乐数据变化
- 调用Lists.getSortedMusicListForAllMusic处理音乐列表排序
- 提供setMusicDataSource方法更新音乐数据源并刷新列表

### 2. UI组件初始化（finishSetup方法）
- **RecyclerView**：展示音乐列表，使用AllMusicAdapter
- **FastScroller**：快速滚动组件，使用Md2风格
- **Shuffle FAB**：显示音乐数量，点击触发随机播放功能
- **搜索工具栏**：包含搜索框和排序菜单

### 3. 搜索功能
- 实现SearchView.OnQueryTextListener接口
- onQueryTextChange：根据搜索文本过滤音乐列表
- 搜索时隐藏排序菜单，聚焦时显示

### 4. 排序功能
- 支持多种排序方式（默认、升序、降序、按添加日期、按艺术家、按专辑等）
- 通过菜单选项切换排序方式
- 保存排序偏好到GoPreferences

### 5. 音乐列表适配器（AllMusicAdapter）
- 继承RecyclerView.Adapter，实现PopupTextProvider（快滚提示）
- 视图持有者（SongsHolder）负责绑定音乐数据到UI
- 显示音乐信息：标题、艺术家&专辑、时长&添加日期

### 6. 交互事件
- 点击音乐项：触发播放选中的音乐
- 长按音乐项：显示音乐操作弹窗（Popups.showPopupForSongs）
- 随机播放按钮：触发所有音乐随机播放
- 导航按钮：关闭当前活动
- 睡眠定时器菜单：打开睡眠定时器对话框

### 7. 其他功能
- 支持音乐可视化变化时更新列表（onSongVisualizationChanged）
- 睡眠定时器图标状态更新（tintSleepTimerIcon）
- 快滚提示文本生成（getPopupText）

## 静态方法
- newInstance：创建AllMusicFragment实例的工厂方法
