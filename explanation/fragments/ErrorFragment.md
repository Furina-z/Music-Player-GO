# ErrorFragment 功能说明

## 基本信息
- 类名：ErrorFragment
- 父类：Fragment
- 用途：用于在应用中显示各种错误状态的片段组件

## 核心功能
- 根据不同错误类型展示对应的错误图标和错误信息
- 提供与宿主Activity的交互能力，支持关闭活动操作

## 关键属性
- _errorFragmentBinding：视图绑定对象，用于操作布局元素
- mUIControlInterface：与宿主Activity通信的接口实例
- mErrorString：错误提示文本的资源ID，默认值为R.string.perm_rationale
- mErrorIcon：错误图标资源ID，默认值为R.drawable.ic_folder_music

## 生命周期方法
1. onAttach(context: Context)
   - 从arguments中获取错误类型参数(TAG_ERROR)
   - 根据错误类型设置对应的错误图标和文本：
     - GoConstants.TAG_NO_MUSIC：设置图标为R.drawable.ic_music_off，文本为R.string.error_no_music
     - GoConstants.TAG_NO_MUSIC_INTENT：设置图标为R.drawable.ic_mood_bad，文本为R.string.error_unknown_unsupported
     - GoConstants.TAG_SD_NOT_READY：设置图标为R.drawable.ic_mood_bad，文本为R.string.error_not_ready
   - 初始化与宿主Activity的通信接口UIControlInterface

2. onCreateView：初始化视图绑定，返回根视图

3. onViewCreated：设置视图内容
   - 绑定错误文本和图标到布局
   - 设置根视图点击事件：调用mUIControlInterface.onCloseActivity()关闭活动
   - 设置工具栏导航按钮点击事件：调用mUIControlInterface.onCloseActivity()关闭活动

4. onDestroyView：释放视图绑定资源

## 实例创建
- 提供newInstance(errorType: String)工厂方法
- 通过bundle传递错误类型参数(TAG_ERROR)

## 常量定义
- TAG_ERROR：参数键名，值为"WE_HAVE_A_PROBLEM_HOUSTON"，用于传递错误类型
