# MediaButtonReceiver.kt 功能解释

1. 类定义与继承：
   - 定义了 MediaButtonReceiver 类，继承自 Android 的 BroadcastReceiver（广播接收器），用于接收和处理系统广播事件。

2. 核心功能：
   - 主要用于处理媒体按钮事件（如耳机线控、蓝牙设备的播放/暂停、上一曲/下一曲等按钮）。

3. onReceive 方法逻辑：
   - 重写 BroadcastReceiver 的 onReceive 方法，该方法在接收到广播时触发。
   - 通过 MediaPlayerHolder.getInstance() 获取媒体播放器的单例实例。
   - 调用 isCurrentSong 检查是否存在当前正在播放的歌曲。
   - 若存在当前歌曲，则调用 handleMediaButton(intent) 处理接收到的媒体按钮意图（intent 中包含具体的媒体按钮事件信息）。

4. 参考来源：
   - 代码注释中提到参考了 Auxio 项目的 MediaButtonReceiver 实现，说明其设计可能借鉴了该项目的媒体按钮处理逻辑。
