# Note
### Bug
「按住按鍵不放」時，`playing` 時的樣式（黃框）不會 remove（但「快速連擊」不會有問題）。
#### 原因
- transition 結束「後」（`transitionend` 事件) 才會執行 `removeTransition()` 。
- 快速點擊時，人為快速點擊的極限約為每秒 5-8 次，每次皆為獨立的事件。
- 持續按壓時，每 30-50ms 觸發一次 `keydown` 事件（約每秒 20-30 次）。但實際可能只播放 5 次。
- 由於上述原因，`transition` 效果無法完整執行；連帶影響 `transitionend` 事件的觸發，及 `removeTransition()`。
#### 解決方法
- 監聽事件從 `keydown` 轉為 `keyup`。
