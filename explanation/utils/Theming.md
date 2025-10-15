# Theming工具类功能总结

## 主题切换与应用
- `applyChanges(activity: Activity, currentViewPagerItem: Int)`：重启MainActivity以应用主题变化，保留当前ViewPager选中项
- `getDefaultNightMode(context: Context)`：根据偏好设置返回默认夜间模式（浅色/深色/跟随系统/自动电池模式）

## 主题状态判断
- `isThemeNight(resources: Resources)`：判断当前是否为夜间模式
- `isThemeBlack(resources: Resources)`：判断当前是否为黑色主题（夜间模式且偏好设置为黑色主题）
- `isDeviceLand(resources: Resources)`：判断设备是否为横屏状态

## 主题样式与颜色处理
- 内部维护`styles`和`stylesBlack`数组：存储不同 accent 颜色对应的主题样式
- `resolveTheme(context: Context)`：根据当前主题状态（黑色/非黑色）和accent偏好返回对应的主题样式
- `resolveThemeColor(resources: Resources)`：根据accent偏好返回对应的主题颜色
- `resolveWidgetsColorNormal(context: Context)`：获取正常状态下控件的颜色
- `resolveColorAttr(context: Context, @AttrRes colorAttr: Int)`：解析主题中的颜色属性值
- `resolveThemeAttr(context: Context, @AttrRes attrRes: Int)`：解析主题中的属性

## 图标与资源获取
- 排序图标：`getSortIconForSongs(sort: Int)`和`getSortIconForSongsDisplayName(sort: Int)`根据排序方式返回对应图标
- 标签相关：`getTabIcon(tab: String)`返回标签对应的图标；`getTabAccessibilityText(tab: String)`返回标签的无障碍文本
- 音量图标：`getPreciseVolumeIcon(volume: Int)`根据音量值返回对应音量图标
- 通知相关：`getNotificationActionTitle(action: String)`返回通知动作标题；`getNotificationActionIcon(action: String, isNotification: Boolean)`返回通知动作图标
- 重复图标：`getRepeatIcon(isNotification: Boolean)`根据重复模式返回对应图标
- 收藏图标：`getFavoriteIcon(isNotification: Boolean)`根据当前歌曲是否为收藏返回对应图标

## 其他功能
- `getAlbumCoverAlpha(context: Context)`：根据主题状态返回专辑封面的透明度值
- `tintSleepTimerMenuItem(tb: MaterialToolbar, isEnabled: Boolean)`：根据启用状态设置睡眠计时器菜单项的图标颜色
- `getOrientation()`：根据旋转锁定偏好返回屏幕方向设置
- `getAccentName(resources: Resources, position: Int)`：根据位置返回accent颜色的名称
