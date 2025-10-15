# BaseActivity.kt 代码功能总结

## 类基本信息
- 类名：BaseActivity
- 类型：抽象类
- 父类：AppCompatActivity
- 作用：作为应用中其他Activity的基类，提供通用功能

## 重写方法及功能

### 1. onStart() 方法
- 重写父类的onStart()方法
- 功能：根据应用主题设置状态栏颜色
  - 调用Theming.isThemeBlack(resources)判断是否为黑色主题
  - 若是黑色主题，将窗口状态栏颜色设置为黑色（Color.BLACK）

### 2. attachBaseContext() 方法
- 重写父类的attachBaseContext()方法，用于处理上下文的本地化配置
- 功能：根据偏好设置或系统默认语言环境更新上下文
  - 初始化应用偏好设置（GoPreferences.initPrefs(newBase)）
  - 若偏好设置中存在保存的语言（locale），使用该语言标签创建Locale对象，并用其更新上下文
  - 若偏好设置中无保存的语言，获取系统配置的默认语言环境（sysLocales[0]），用其更新上下文
  - 若系统无默认语言环境，使用Locale.getDefault()更新上下文
  - 最终调用父类方法附加更新后的上下文
