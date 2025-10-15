### Sorting.kt 代码功能解释

1. **包声明**：属于 `com.iven.musicplayergo.models` 包，表明这是音乐播放器应用中的一个模型类。

2. **依赖导入**：导入 `com.squareup.moshi.JsonClass`，用于结合 Moshi 库进行 JSON 数据的序列化与反序列化。

3. **Moshi 注解**：`@JsonClass(generateAdapter = true)` 注解表示 Moshi 会为该数据类自动生成 JSON 适配器，方便将该类对象与 JSON 数据互相转换。

4. **数据类定义**：`data class Sorting` 是一个 Kotlin 数据类，用于存储排序相关的配置信息，包含以下属性：
   - `albumOrFolder: String?`：可空字符串，可能表示专辑或文件夹的排序相关参数（如排序依据）
   - `launchedBy: String`：非空字符串，可能表示该排序配置的启动来源（如哪个模块或操作触发）
   - `songVisualization: String?`：可空字符串，可能与歌曲可视化展示的排序方式相关
   - `sorting: Int`：整数类型，可能表示具体的排序方式标识（如 0 代表按名称排序，1 代表按时间排序等）
