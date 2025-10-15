# PreferencesFragment 功能说明

## 基本信息
- 类名：PreferencesFragment
- 父类：PreferenceFragmentCompat
- 实现接口：SharedPreferences.OnSharedPreferenceChangeListener, Preference.OnPreferenceClickListener
- 用途：处理应用偏好设置界面的展示与交互

## 核心功能

### 1. 生命周期与初始化
- onResume()：注册SharedPreferences变化监听
- onPause()：注销SharedPreferences变化监听
- onAttach()：绑定UI控制接口（UIControlInterface）和媒体控制接口（MediaControlInterface）
- onViewCreated()：初始化偏好项的UI（图标、可见性、摘要、点击监听等）
- onCreatePreferences()：从XML资源加载偏好设置布局（R.xml.preferences）

### 2. 偏好项UI配置
- 主题偏好：根据当前主题设置图标（日/夜模式）
- 黑色主题偏好：仅在夜间模式下可见
- 强调色偏好：显示当前强调色名称，设置点击监听
- 过滤偏好：显示过滤数量摘要，设置点击监听，无过滤时禁用
- 活动标签偏好：显示活动标签数量摘要，设置点击监听
- 通知操作偏好：显示当前通知操作标题，设置点击监听
- 重置排序偏好：根据是否有排序设置决定是否启用，设置点击监听

### 3. 偏好点击事件处理（onPreferenceClick）
- 强调色偏好：显示颜色选择底部表单（RecyclerSheet.ACCENT_TYPE）
- 活动标签偏好：显示标签选择底部表单（RecyclerSheet.TABS_TYPE）
- 过滤偏好：显示过滤设置底部表单（RecyclerSheet.FILTERS_TYPE，仅当有过滤时）
- 通知操作偏好：显示通知操作选择底部表单（RecyclerSheet.NOTIFICATION_ACTIONS_TYPE）
- 重置排序偏好：显示重置排序对话框

### 4. 偏好变化监听（onSharedPreferenceChanged）
- 精确音量偏好：更新媒体播放器音量（切换精确音量模式）
- 播放速度偏好：通知媒体控制接口切换播放速度
- 主题偏好：通知UI接口更新外观（主题改变）
- 黑色主题偏好：通知UI接口更新外观（非主题改变）
- 均衡器偏好：启用/释放内置均衡器
- 音频焦点偏好：获取/放弃音频焦点
- 封面偏好：通知媒体控制接口更新封面设置
- 通知操作偏好：更新通知操作偏好的摘要
- 歌曲视觉偏好：更新媒体会话元数据，通知更新播放中的专辑歌曲
- 旋转偏好：更新Activity的屏幕方向
- 详情排序偏好：更新重置排序选项状态，更新媒体会话元数据，通知更新播放中的专辑歌曲

### 5. 辅助方法
- enableEqualizerOption()：更新均衡器开关偏好的状态（启用/禁用、勾选状态、摘要）
- updateResetSortingsOption()：根据排序设置状态更新重置排序偏好的启用状态

### 6. 实例创建
- newInstance()：静态工厂方法，用于创建PreferencesFragment实例
