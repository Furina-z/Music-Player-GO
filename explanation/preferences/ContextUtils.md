# 类：ContextUtils

## 基本信息
- 包路径：com.iven.musicplayergo.preferences
- 父类：ContextWrapper
- 用途：处理Android应用的语言切换及支持的语言列表相关功能


## 伴生对象方法：updateLocale

### 功能
根据指定的Locale更新上下文（Context）的语言环境，实现应用内语言切换。

### 参数
- ctx：当前上下文（Context）
- localeToSwitchTo：目标切换的语言环境（Locale）

### 实现细节
1. 针对不同Android版本做适配处理：
   - Android N（API 24）及以上：
     - 创建包含目标Locale的LocaleList
     - 设置LocaleList为默认
     - 更新配置中的语言列表（configuration.setLocales）
     - 通过createConfigurationContext创建新上下文
   - Android N以下：
     - 直接设置配置的locale（configuration.locale）
     - 调用resources.updateConfiguration更新资源配置
2. 返回包装了新上下文的ContextUtils实例


## 伴生对象方法：getLocalesList

### 功能
获取应用支持的语言列表，以语言代码为键、语言名称为值的有序Map形式返回。

### 参数
- resources：应用资源（Resources）

### 实现细节
1. 从资源文件中获取：
   - 支持的语言代码数组（R.array.supported_locales）
   - 对应的语言名称数组（R.array.supported_locales_names）
2. 将两个数组通过zip配对成Map
3. 按语言名称（value）排序后，以Map形式返回
