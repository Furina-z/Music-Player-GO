## Permissions工具类功能总结

1. **权限常量定义**  
   - 定义`PERMISSION_READ_AUDIO`属性，根据Android版本返回对应的音频读取权限：Android 13及以上（Tiramisu）使用`Manifest.permission.READ_MEDIA_AUDIO`，低版本使用`Manifest.permission.READ_EXTERNAL_STORAGE`。

2. **权限判断方法**  
   - `hasToAskForReadStoragePermission(activity: Activity)`：判断是否需要请求存储读取权限。当Android版本为6.0及以上（Marshmallow）且未授予`PERMISSION_READ_AUDIO`权限时，返回true。

3. **权限请求管理**  
   - `manageAskForReadStoragePermission(activity: Activity)`：管理存储权限的请求流程。  
     - 若系统建议显示权限请求理由（`shouldShowRequestPermissionRationale`返回true），则弹出Material对话框解释权限用途，用户点击"确定"则发起权限请求，点击"取消"则调用`UIControlInterface`的`onDenyPermission`方法。  
     - 若无需显示理由，则直接发起权限请求。

4. **权限请求实现**  
   - 私有方法`askForReadStoragePermission(activity: Activity)`：实际发起权限请求，调用`ActivityCompat.requestPermissions`，请求`PERMISSION_READ_AUDIO`权限，请求码为`GoConstants.PERMISSION_REQUEST_READ_EXTERNAL_STORAGE`。
