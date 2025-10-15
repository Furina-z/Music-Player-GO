# Music.kt功能解释

- **类功能**：`Music` 是一个数据类，用于封装音乐文件的相关信息，方便在音乐播放器应用中存储和传递音乐元数据及关联属性。
- **注解说明**：`@JsonClass(generateAdapter = true)` 表示通过 Moshi 库为该类生成 JSON 适配器，支持该类与 JSON 数据之间的序列化和反序列化操作。
- **属性说明**：
  - `artist: String?`：音乐的艺术家（歌手）名称，可为空
  - `year: Int`：音乐的发行年份
  - `track: Int`：音乐在专辑中的曲目编号
  - `title: String?`：音乐的标题名称，可为空
  - `displayName: String?`：音乐的显示名称（可能与标题不同），可为空
  - `duration: Long`：音乐的时长（单位通常为毫秒）
  - `album: String?`：音乐所属专辑的名称，可为空
  - `albumId: Long?`：音乐所属专辑的ID，可为空
  - `relativePath: String?`：音乐文件的相对路径，可为空
  - `id: Long?`：音乐的唯一标识ID，可为空
  - `launchedBy: String`：启动该音乐的来源信息
  - `startFrom: Int`：音乐开始播放的起始位置（单位通常为毫秒）
  - `dateAdded: Int`：音乐添加到应用的日期（通常为时间戳）
