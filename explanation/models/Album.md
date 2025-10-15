# Album.kt 功能解释

## 类用途
`Album` 是一个 Kotlin 数据类（data class），位于 `com.iven.musicplayergo.models` 包下，主要用于存储音乐专辑的相关信息。

## 属性说明
- `title: String?`：专辑标题，可为空（表示可能没有标题信息）
- `year: String?`：专辑发行年份，可为空（表示可能没有年份信息）
- `music: MutableList<Music>?`：专辑包含的音乐列表，类型为可修改的 `Music` 对象列表，可为空（表示可能没有音乐信息）
- `totalDuration: Long`：专辑的总时长，以长整型（Long）表示（不可为空，需提供具体时长值）
