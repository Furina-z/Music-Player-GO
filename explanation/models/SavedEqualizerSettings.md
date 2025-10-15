# SavedEqualizerSettings.kt功能解析

SavedEqualizerSettings.kt 是一个数据类，用于存储音乐播放器的均衡器相关设置，位于 com.iven.musicplayergo.models 包下。

## 功能说明：
- 作为均衡器设置的数据模型，用于保存均衡器的各项配置信息
- 通过 @JsonClass(generateAdapter = true) 注解，支持使用 Moshi 库进行 JSON 序列化和反序列化，便于将设置数据进行持久化存储或传输

## 属性说明：
- enabled: Boolean - 标识均衡器是否启用
- preset: Int - 表示选中的均衡器预设模式（如不同音效预设）
- bandsSettings: List<Short>? - 各个均衡器频段的具体设置值，可为 null
- bassBoost: Short - 低音增强的强度设置
- virtualizer: Short - 虚拟环绕声的强度设置
