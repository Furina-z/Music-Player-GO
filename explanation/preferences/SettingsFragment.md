# SettingsFragment 功能解释

## 基本信息
- 类名：`SettingsFragment`
- 类型：`Fragment` 子类，用于应用的设置页面
- 作用：展示应用设置界面，包含偏好设置、语言切换、GitHub页面跳转等功能

## 核心变量
- `_fragmentSettingsBinding`：视图绑定对象，用于访问布局控件
- `mUIControlInterface`：UI控制接口，用于与宿主Activity交互
- `mPreferencesFragment`：偏好设置碎片，展示具体的设置选项

## 生命周期方法
1. `onAttach`：绑定宿主Activity，获取`UIControlInterface`实例，确保Activity实现该接口
2. `onDestroyView`：释放视图绑定对象，避免内存泄漏
3. `onCreateView`：初始化视图绑定，返回布局根视图
4. `onViewCreated`：初始化视图内容，设置工具栏和加载偏好设置碎片

## 主要功能方法
1. `getPreferencesFragment`：返回偏好设置碎片实例

2. `openLocaleSwitcher`：
   - 获取可用语言列表
   - 创建语言选择对话框，展示可选语言
   - 选择语言后更新偏好设置，并通过`mUIControlInterface`通知UI更新
   - 提供"默认"选项，用于重置语言设置

3. `openGitHubPage`：
   - 使用`CustomTabsIntent`构建自定义标签页意图
   - 尝试用自定义标签页打开GitHub链接
   - 若失败，使用普通浏览器意图打开链接
   - 若没有可用浏览器，显示错误提示

4. `solveInfo`：
   - 查询能处理指定意图的活动列表
   - 适配Android Tiramisu及以下版本，处理不同的`PackageManager`查询方式

5. 工具栏设置：
   - 加载设置菜单（包含GitHub页面和语言切换选项）
   - 设置导航按钮点击事件（关闭当前活动）
   - 设置菜单 item 点击事件（触发对应功能）

## 其他
- `companion object`：提供`newInstance`方法，用于创建`SettingsFragment`实例
- 布局相关：通过`FragmentSettingsBinding`绑定布局，将`PreferencesFragment`加载到`fragment_layout`容器中
