# ViewExts.kt 扩展函数功能说明

## 视图边距调整
- `View.applyEdgeToEdge()`：设置视图应用边到边显示，通过监听窗口内边距（systemBars），调整视图左右内边距以适配系统栏。

## 图片加载
- `ImageView.loadWithError(bitmap: Bitmap?, error: Boolean, albumArt: Int)`：根据错误状态加载图片。若出错，使用指定资源的图片并设置居中显示；否则加载指定 bitmap 并设置居中裁剪。

## Toolbar 相关
- `Toolbar.getTitleTextView()`：通过反射获取 Toolbar 中的标题 TextView（mTitleTextView 字段）。

## 菜单相关
- `MenuItem.setTitleColor(color: Int)`：给菜单项标题设置前景色，通过 SpannableString 实现。
- `MenuItem.setIconTint(color: Int)`：给菜单项图标设置 tint 颜色，通过包装 Drawable 实现。
- `MenuItem.setTitle(resources: Resources, title: String?)`：给菜单项标题设置相对大小（0.75f）和主题颜色，通过 SpannableString 实现。
- `Menu.enablePopupIcons(resources: Resources)`：对 MenuBuilder 类型的菜单，设置可选图标可见，并给图标添加左右内边距。

## Fragment 管理
- `FragmentManager.addFragment(fragment: Fragment?, tag: String?)`：向容器添加 fragment，并加入返回栈。
- `FragmentManager.goBackFromFragmentNow(fragment: Fragment?)`：从 fragment 返回，移除指定 fragment 并立即弹出返回栈。
- `FragmentManager.isFragment(fragmentTag: String)`：判断指定 tag 的 fragment 是否可见且已添加。

## 动画相关
- `View.createCircularReveal(show: Boolean)`：创建圆形揭露动画。根据 show 参数决定是显示（从 0 到最大半径）还是隐藏（从最大半径到 0），并伴随背景色动画。
- `View.slide(show: Boolean)`：创建顶部滑入/滑出动画，通过 Slide 过渡实现视图显示/隐藏。

## RecyclerView 相关
- `RecyclerView.smoothSnapToPosition(position: Int)`：平滑滚动到指定位置并触发点击事件，通过 LinearSmoothScroller 实现。
- `RecyclerView.disableScrollbars()`：禁用 RecyclerView的垂直和水平滚动条。

## 视图可见性与点击
- `View.handleViewVisibility(show: Boolean)`：根据 show 参数设置视图可见性（VISIBLE/GONE）。
- `View.safeClickListener(safeClickListener: (view: View) -> Unit)`：设置安全点击监听器，通过 SingleClickHelper 防止快速重复点击。

## 图片视图 tint
- `ImageView.updateIconTint(tint: Int)`：更新 ImageView 的图标 tint 颜色，使用 ColorStateList。

## 对话框相关
- `Dialog?.applyFullHeightDialog(activity: Activity)`：设置对话框为全屏高度，通过获取窗口 metrics 调整 BottomSheet 的 peekHeight。
- `Dialog?.disableShapeAnimation()`：禁用 BottomSheetDialog 的形状动画（通过反射调用 disableShapeAnimations()）。

## ViewPager2 相关
- `ViewPager2.reduceDragSensitivity()`：降低 ViewPager2 的拖拽敏感度，通过反射修改内部 RecyclerView的 mTouchSlop 值（乘以3），减少垂直滚动被误判为水平滑动的情况。
