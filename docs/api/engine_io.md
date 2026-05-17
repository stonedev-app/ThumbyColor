# engine_io — 入力・デバイス制御

公式ドキュメント: https://color.thumby.us/doc/build/engine_io.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_io as btn
from engine_io import rumble
```

**ボタン**: `btn.UP`, `btn.DOWN`, `btn.LEFT`, `btn.RIGHT`, `btn.A`, `btn.B`, `btn.LB`, `btn.RB`, `btn.MENU`

| プロパティ | 説明 |
|-----------|------|
| `.is_just_pressed` | このフレームで押された |
| `.is_pressed` | 押し続けている |
| `.is_long_pressed` | 長押し中 |
| `.is_just_released` | このフレームで離した |

`rumble(intensity)` — バイブレーション（0.0〜1.0、0で停止）

その他:
- `battery_level()` — バッテリー残量取得
- `is_plugged_in()` — USB接続確認
- `focused_node()` — GUI フォーカス中のノードを取得

## 使用例

```python
import engine_main
import engine
import engine_io as btn
from engine_io import rumble
from engine_nodes import Sprite2DNode
from engine_math import Vector2

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)
        self.position = Vector2(0, 0)

    def tick(self, dt):
        speed = 60  # px/秒
        if btn.LEFT.is_pressed:
            self.position.x -= speed * dt
        if btn.RIGHT.is_pressed:
            self.position.x += speed * dt
        if btn.UP.is_pressed:
            self.position.y += speed * dt
        if btn.DOWN.is_pressed:
            self.position.y -= speed * dt
        if btn.A.is_just_pressed:
            rumble(0.5)  # 短い振動
        if btn.A.is_just_released:
            rumble(0)    # 振動停止
```
