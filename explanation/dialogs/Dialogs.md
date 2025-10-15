### 核心功能
该文件通过一个`object`类型的`Dialogs`单例，提供了一系列静态方法（用`@JvmStatic`标注），用于创建并显示符合Material Design风格的对话框，涵盖了清除数据、停止播放、排序设置等多种场景，且会根据应用偏好设置（如是否需要确认操作）决定是否弹出确认对话框。


### 主要方法及作用
1. **`showClearFiltersDialog(activity: Activity)`**  
   显示“清除过滤器”对话框。若应用偏好设置中`isAskForRemoval`为`true`，则弹出确认对话框（包含“是”“否”按钮），用户确认后通过`UIControlInterface`的`onFiltersCleared`方法清除过滤器；否则直接执行清除操作。


2. **`showClearQueueDialog(context: Context)`**  
   显示“清除播放队列”对话框。逻辑与清除过滤器类似：根据`isAskForRemoval`判断是否需要确认，确认后会清除偏好设置中的队列数据，并通过`MediaPlayerHolder`清空播放队列、更新队列状态。


3. **`showClearFavoritesDialog(activity: Activity)`**  
   显示“清除收藏”对话框。根据`isAskForRemoval`决定是否弹出确认，确认后通过`UIControlInterface`的`onFavoritesUpdated`方法（参数`clear = true`）清除所有收藏。


4. **`stopPlaybackDialog(context: Context)`**  
   显示“停止播放”对话框（不可取消）。包含三个按钮：  
   - “是”：通过`MediaPlayerHolder`停止播放服务；  
   - “否”：不停止播放服务；  
   - “取消”：关闭对话框。  
   若`isAskForRemoval`为`false`，则直接执行“不停止播放服务”的逻辑。


5. **`showSaveSortingDialog(activity: Activity, artistOrFolder: String?, launchedBy: String, sorting: Int)`**  
   显示“保存排序方式”对话框。用于确认排序设置的保存方式，包含三个按钮：  
   - “是”：将排序方式保存为默认排序；  
   - “否”：将排序方式保存到当前艺术家或文件夹；  
   - 中性按钮（“重置”）：重置为默认排序设置。


6. **`showResetSortingsDialog(context: Context)`**  
   显示“重置排序”对话框。根据`isAskForRemoval`判断是否需要确认，确认后清除偏好设置中的排序数据并重置为默认排序。


7. **`computeDurationText(ctx: Context, favorite: Music?): Spanned?`**  
   计算并返回格式化的时长文本（支持HTML格式），用于显示收藏歌曲的时长信息。若歌曲有起始时间（`startFrom > 0`），则显示“起始时间/总时长”；否则直接显示总时长。


### 总结
该文件通过集中管理对话框逻辑，保证了应用内交互风格的一致性，同时通过调用`GoPreferences`（偏好设置）、`MediaPlayerHolder`（播放器核心）、`UIControlInterface`（UI控制接口）等组件，将对话框交互与业务逻辑解耦，提升了代码的可维护性。
