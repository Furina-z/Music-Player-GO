该文件是一个 Android 应用中的EqualizerFragment.kt，主要实现了音乐播放器的均衡器功能界面，负责均衡器相关的 UI 展示、参数调整、设置保存等功能。以下是其核心内容介绍：

### 核心功能
- 管理音乐播放器的均衡器相关功能，包括调整频段水平、低音增强、虚拟环绕声强度
- 支持选择系统预设的均衡器配置，并能实时更新滑块显示
- 提供启用/禁用均衡器的开关控制
- 保存用户的均衡器设置（选中的预设、低音/虚拟器强度）
- 界面加载时的圆形揭露动画效果（当启用动画时）

### 主要变量说明
- _eqFragmentBinding: FragmentEqualizerBinding类型，用于视图绑定，管理布局元素
- mSliders: 可变Map，存储Slider（滑块）与对应的TextView（频率文本）的映射关系
- mEqAnimator: Animator类型，用于界面的圆形揭露动画
- mEqualizer: Triple类型，存储Equalizer（均衡器）、BassBoost（低音增强）、Virtualizer（虚拟器）实例
- mPresetsList: 可变List，存储系统均衡器预设的名称
- mSelectedPreset: Int类型，记录当前选中的预设索引
- mMediaPlayerHolder: 获取MediaPlayerHolder实例，用于管理均衡器初始化、设置保存等
- mGoPreferences: 获取GoPreferences实例，用于读取和保存用户配置

### 生命周期方法
- onDestroyView: 重写父类方法，在视图销毁时调用saveEqSettings保存设置，并置空视图绑定
- onCreateView: 加载布局，初始化视图绑定并返回根视图
- onViewCreated: 视图创建后初始化均衡器，设置低音和虚拟器滑块的监听，加载系统预设列表；若预设列表不为空则完成均衡器设置，否则报错关闭

### 关键方法说明
- saveEqSettings: 保存当前均衡器设置（选中的预设、低音/虚拟器强度）到MediaPlayerHolder
- finishSetupEqualizer: 完成均衡器核心设置，包括绑定滑块与频率文本、设置滑块范围和监听、格式化频率文本、初始化预设下拉框、配置界面动画等
- setupToolbar: 设置工具栏，包括返回按钮和均衡器启用/禁用开关，开关状态与均衡器启用状态同步
- updateBandLevels: 更新所有滑块的水平，根据预设变化或保存的设置调整滑块位置
- formatMilliHzToK: 将毫赫兹（mHz）转换为更易读的单位（Hz或kHz）
- closeEqualizerOnError: 处理均衡器初始化错误，禁用均衡器、释放资源并关闭当前界面
