# GoPreferences 类功能总结

## 基本信息
- 所属包：`com.iven.musicplayergo`
- 作用：用于管理应用的偏好设置，通过 SharedPreferences 存储和读取各类配置信息，支持基本数据类型及复杂对象的持久化。


## 核心功能
1. **偏好设置初始化与单例管理**
   - 通过 `initPrefs(context)` 方法初始化，确保应用中仅存在一个实例（单例模式）
   - 通过 `getPrefsInstance()` 获取已初始化的实例，未初始化时会抛出异常

2. **数据存储与读取**
   - 基于 `SharedPreferences` 存储基本数据类型（int、float、boolean、String、Set<String> 等）
   - 结合 `Moshi` 库实现复杂对象（如 `Music`、`SavedEqualizerSettings`）及集合（如 `List<Music>`、`List<String>`）的 JSON 序列化与反序列化，实现持久化存储


## 主要偏好设置属性
包含以下关键配置项（仅列举部分）：
- **播放相关**：`latestVolume`（最近音量）、`latestPlaybackSpeed`（最近播放速度）、`latestPlayedSong`（最近播放歌曲）、`queue`（播放队列）
- **外观相关**：`theme`（主题）、`isBlackTheme`（是否黑色主题）、`accent`（强调色）、`isAnimations`（是否启用动画）
- **排序相关**：`artistsSorting`（艺术家排序）、`albumsSorting`（专辑排序）、`sortings`（排序设置列表）
- **行为相关**：`onListEnded`（列表结束行为）、`fastSeekingStep`（快进/快退步长）、`isEqForced`（是否强制启用均衡器）
- **其他**：`favorites`（收藏歌曲列表）、`notificationActions`（通知栏操作）、`locale`（语言设置）、`lockRotation`（是否锁定旋转）


## 复杂对象处理方法
- `putObjectForType`/`getObjectForType`：用于存储和读取带泛型的复杂类型（如 `List<String>`、`List<Music>`）
- `putObjectForClass`/`getObjectForClass`：用于存储和读取具体类的对象（如 `Music`、`SavedEqualizerSettings`）
