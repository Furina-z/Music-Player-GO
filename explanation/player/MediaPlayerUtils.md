# MediaPlayerUtils 功能解释

## 1. safePause 方法
- 作用：安全地暂停 MediaPlayer 播放
- 参数：接收一个 MediaPlayer 实例
- 操作：
  - 使用 with 语句简化对 mediaPlayer 的操作
  - 在 try 块中检查 mediaPlayer 是否处于播放状态（isPlaying），如果是则调用 pause() 方法暂停
  - 捕获 IllegalStateException 异常并打印堆栈跟踪，避免因 MediaPlayer 状态异常导致的崩溃

## 2. safePlay 方法
- 作用：安全地启动 MediaPlayer 播放
- 参数：接收一个 MediaPlayer 实例
- 操作：
  - 使用 with 语句简化对 mediaPlayer 的操作
  - 在 try 块中调用 start() 方法启动播放
  - 捕获 IllegalStateException 异常并打印堆栈跟踪，处理 MediaPlayer 状态异常的情况

## 3. safeSetPlaybackSpeed 方法
- 作用：安全地设置 MediaPlayer 的播放速度
- 注解：@TargetApi(Build.VERSION_CODES.M) 表明该方法最低支持 Android 6.0（API 23）
- 参数：
  - mediaPlayer：需要设置速度的 MediaPlayer 实例
  - speed：目标播放速度（Float 类型）
- 操作：
  - 使用 with 语句简化对 mediaPlayer 的操作
  - 在 try 块中通过 playbackParams.setSpeed(speed) 设置播放速度
  - 捕获 IllegalArgumentException 异常：
    - 异常发生时将播放速度重置为 1.0F（正常速度）
    - 打印堆栈跟踪，处理速度参数不合法的情况
