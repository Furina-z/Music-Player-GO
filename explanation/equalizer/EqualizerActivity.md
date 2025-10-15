## EqualizerActivity.kt 功能说明

### 1. 基础信息
- **所属包**：`com.iven.musicplayergo.equalizer`
- **类定位**：音乐播放器应用中与均衡器功能相关的入口Activity，负责承载均衡器界面及基础配置
- **继承关系**：继承自 `BaseActivity`，复用基础Activity的通用逻辑（如生命周期管理、基础初始化等）


### 2. 核心成员变量
- **视图绑定对象**：`mEqualizerBinding`（类型为 `ActivityEqualizerBinding`），用于通过ViewBinding方式安全访问布局控件，替代传统`findViewById`
- **返回键回调**：`onBackPressedCallback`（类型为 `OnBackPressedCallback`），自定义返回键点击行为，初始状态设为`true`（启用回调）


### 3. 关键生命周期与功能实现（onCreate方法）
`onCreate` 是Activity的核心初始化方法，该类在此方法中完成以下关键操作：
1. **主题设置**：  
   通过 `Theming.resolveTheme(this)` 动态获取并设置当前Activity的主题，支持应用自定义主题（如深色/浅色模式、自定义配色等）
2. **视图初始化**：  
   - 调用 `ActivityEqualizerBinding.inflate(layoutInflater)` 加载Activity对应的布局文件（`activity_equalizer.xml`）
   - 通过 `setContentView(mEqualizerBinding.root)` 将加载的布局设置为当前Activity的内容视图
3. **系统版本适配（Android 8.1+）**：  
   针对 API 27（Android O MR1，8.1版本）及以上系统：
   - 调用 `WindowCompat.setDecorFitsSystemWindows(window, true)` 调整窗口装饰与系统窗口的适配关系
   - 调用 `mEqualizerBinding.root.applyEdgeToEdge()` 执行边缘到边缘布局适配（通常用于全面屏，让界面延伸至状态栏/导航栏区域）
4. **返回键行为绑定**：  
   通过 `onBackPressedDispatcher.addCallback(this, onBackPressedCallback)` 将自定义返回键回调绑定到当前Activity，实现返回键逻辑自定义


### 4. 自定义返回键逻辑
`onBackPressedCallback` 的 `handleOnBackPressed` 方法定义返回键行为：  
- 调用 `finishAndRemoveTask()`：结束当前Activity，并移除整个任务栈（确保退出后该Activity及关联任务不会保留在后台任务列表中，彻底退出均衡器功能页面）


### 5. 整体作用总结
该类是均衡器功能的入口载体，核心职责包括：
- 初始化均衡器界面的布局与视图绑定
- 适配不同系统版本的窗口显示规则（尤其是全面屏边缘适配）
- 自定义返回键行为，保证退出逻辑符合应用交互规范
- 继承基础Activity，复用通用初始化逻辑，减少代码冗余
