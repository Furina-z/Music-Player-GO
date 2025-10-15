# GoApp类功能总结

## 类定义
- 类名：`GoApp`
- 继承关系：继承自`Application`类
- 实现接口：实现`ImageLoaderFactory`接口，用于提供Coil图像加载器配置

## onCreate方法功能
- 重写`Application`的`onCreate`方法，在应用启动时执行初始化操作
- 调用`GoPreferences.initPrefs(applicationContext)`初始化应用偏好设置
- 通过`AppCompatDelegate.setDefaultNightMode`方法，结合`Theming.getDefaultNightMode(applicationContext)`设置应用默认的夜间模式

## newImageLoader方法功能
- 实现`ImageLoaderFactory`接口的`newImageLoader`方法，提供自定义的Coil图像加载器配置
- 配置内容包括：
  - 禁用磁盘缓存（`diskCachePolicy(CachePolicy.DISABLED)`）
  - 启用图像加载时的淡入淡出过渡效果（`crossfade(true)`）
