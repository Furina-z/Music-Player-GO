# MusicUtils.kt 功能总结

## 概述
该文件是一个音乐相关的工具类（`object MusicUtils`），包含一系列静态方法，主要用于处理音乐专辑、歌曲的查询、排序、过滤以及媒体播放器列表更新等操作，服务于音乐播放器应用的功能实现。

## 主要方法功能

1. **getPlayingAlbumPosition**  
   根据选中的艺术家（`selectedArtist`）和设备上按艺术家分类的专辑列表（`deviceAlbumsByArtist`），获取当前播放专辑在列表中的位置。若选中的艺术家与当前播放歌曲的艺术家不同，返回`RecyclerView.NO_POSITION`（无效位置）。

2. **getAlbumSongs**  
   根据艺术家（`artist`）、专辑名（`album`）和设备专辑列表（`deviceAlbumsByArtist`），获取指定专辑下的歌曲列表。

3. **getAlbumFromList**  
   从指定艺术家的专辑列表中，根据专辑名（`album`）查询对应的专辑对象及其在列表中的位置，返回包含专辑和位置的`Pair`。若查询失败（如专辑不存在），返回列表中第一个专辑及位置0。

4. **buildSortedArtistAlbums**  
   根据艺术家的歌曲列表（`artistSongs`）构建专辑列表。先按专辑名分组歌曲，每组内歌曲按曲目号（`track`）排序，再为每个专辑创建`Album`对象（包含专辑名、年份、歌曲列表、总时长），最后将所有专辑按年份排序并返回。

5. **updateMediaPlayerHolderLists**  
   更新媒体播放器（`MediaPlayerHolder`）的歌曲列表，处理过滤条件（`filters`）：  
   - 移除收藏歌曲中符合过滤条件的歌曲，并通知UI更新收藏状态；  
   - 若播放队列中存在符合过滤条件的歌曲，移除它们并跳至下一首；  
   - 若当前播放歌曲符合过滤条件，尝试选择新歌曲（`randomMusic`）作为播放曲目。

6. **musicListContains**  
   判断歌曲（`song`）是否包含在过滤条件（`filter`）中，检查歌曲的艺术家、专辑或相对路径是否在过滤集合内，返回布尔值。
