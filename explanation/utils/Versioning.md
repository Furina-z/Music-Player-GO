# Versioning工具类功能总结

该工具类用于判断当前Android设备的系统版本是否达到或超过特定版本，具体功能如下：

- 提供`isQ()`方法：判断设备系统版本是否达到或超过Android Q（Android 10，对应SDK_INT >= 29）
- 提供`isMarshmallow()`方法：判断设备系统版本是否达到或超过Android Marshmallow（Android 6.0，对应SDK_INT >= 23）
- 提供`isTiramisu()`方法：判断设备系统版本是否达到或超过Android Tiramisu（Android 13，对应SDK_INT >= 33）
