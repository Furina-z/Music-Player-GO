# SingleClickHelper 功能总结

## 作用
用于防止短时间内的重复点击操作，避免因快速多次点击导致的意外行为。

## 核心常量
- `MIN_CLICK_INTERVAL`：最小点击间隔时间，默认值为500毫秒，即两次有效点击之间的最小时间差。

## 主要方法
1. `isBlockingClick(): Boolean`
   - 无参方法，调用带参的`isBlockingClick`方法，传入默认的`MIN_CLICK_INTERVAL`（转换为Long类型）。
   - 返回值表示当前点击是否需要被阻塞（即是否为短时间内的重复点击）。

2. `isBlockingClick(minClickInterval: Long): Boolean`（私有）
   - 带参方法，接收自定义的最小点击间隔时间。
   - 逻辑：
     - 获取当前系统时间。
     - 计算当前时间与上次点击时间（`sLastClickTime`）的差值绝对值。
     - 若差值小于最小点击间隔，则判定为需要阻塞当前点击（返回true）。
     - 若差值不小于最小点击间隔，则更新上次点击时间为当前时间，并判定为不需要阻塞（返回false）。
