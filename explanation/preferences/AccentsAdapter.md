# AccentsAdapter.kt 功能说明

## 一、类定义与初始化
- 所属包：com.iven.musicplayergo.preferences
- 继承关系：继承自 RecyclerView.Adapter<AccentsAdapter.AccentsHolder>，用于适配RecyclerView展示accent颜色选项
- 构造参数：接收IntArray类型的accents，存储所有可选的accent颜色值
- 选中状态变量：selectedAccent，初始值从GoPreferences.getPrefsInstance().accent获取，记录当前选中的accent位置

## 二、视图Holder相关方法
1. onCreateViewHolder：通过AccentItemBinding加载item布局（从parent上下文的LayoutInflater），创建并返回AccentsHolder实例
2. getItemCount：返回accents数组的长度，即accent选项的数量
3. onBindViewHolder：调用holder的bindItems方法，将当前位置的accent颜色（accents[holder.absoluteAdapterPosition]）绑定到视图

## 三、AccentsHolder的bindItems方法（item绑定逻辑）
1. 内容描述设置：通过Theming.getAccentName获取当前位置accent的全名，设置为item的contentDescription
2. 卡片背景色：将item的卡片背景色设置为传入的color（当前accent颜色）
3. 样式设置（根据是否选中）：
   - 非选中项（absoluteAdapterPosition != selectedAccent）：strokeWidth设为0，圆角半径使用R.dimen.accent_radius
   - 选中项（absoluteAdapterPosition == selectedAccent）：strokeWidth设为R.dimen.accent_stroke；根据color的亮度（ColorUtils.calculateLuminance）确定边框色（亮度<0.35用Color.WHITE，否则用Color.DKGRAY），并设置透明度为75；圆角半径使用R.dimen.accent_radius_alt
4. 点击事件：当点击的位置不是当前选中项时，先通知适配器刷新旧选中项（notifyItemChanged(selectedAccent)），更新selectedAccent为当前位置，再通知刷新新选中项（notifyItemChanged(absoluteAdapterPosition)）
5. 长按事件：显示包含当前accent全名的Toast（时长LENGTH_SHORT），并返回true表示消费事件
