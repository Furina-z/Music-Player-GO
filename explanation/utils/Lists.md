# Lists工具类功能总结

## 一、列表过滤功能
- `processQueryForStringsLists`：对字符串列表进行查询过滤，支持不区分大小写的包含匹配
- `processQueryForMusic`：对音乐列表进行查询过滤，根据显示设置（文件名或标题）进行不区分大小写的包含匹配

## 二、列表排序功能
### 1. 字符串列表排序
- `getSortedList`：根据排序ID对字符串列表进行升序或降序排序
- `getSortedListWithNull`：处理含null的字符串列表（null转为空字符串）后，按指定排序ID排序
- `transformNullToEmpty`：将null转换为空字符串的辅助方法

### 2. 音乐列表排序
- `getSortedMusicList`：根据排序ID对音乐列表排序（支持按显示设置升序/降序、曲目号正序/倒序）
- `getSortedMusicListForFolder`：针对文件夹内音乐列表排序（支持按文件名、添加日期、艺术家等升序/降序）
- `getSortedMusicListForAllMusic`：针对所有音乐列表排序（支持更多维度如专辑等的升序/降序）
- `getSortedListBySelectedVisualization`：根据显示设置（文件名或标题）对音乐列表升序排序

## 三、排序相关辅助功能
- `getSelectedSorting`：根据排序ID获取菜单中对应的选中项
- `getSelectedSortingForMusic`：针对音乐排序，根据排序ID获取菜单中对应的选中项
- `getSongsSorting`：切换歌曲排序模式（循环切换曲目号正序/倒序、升序/降序）
- `getSongsDisplayNameSorting`：切换按显示名排序的模式（升序与降序互转）
- `getDefSortingMode`：根据显示设置获取默认排序模式
- `getUserSorting`：获取用户针对特定来源的排序设置

## 四、偏好设置相关功能
- `hideItems`：将指定项目添加到隐藏列表（过滤器）并更新偏好设置
- `addToFavorites`：添加或移除歌曲到收藏列表，并显示相应提示信息
- `addToSortings`：添加或更新排序设置，并通知界面更新排序状态
