# engine_animation — アニメーション（Tween）

公式ドキュメント: https://color.thumby.us/doc/build/engine_animation.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
from engine_animation import Tween, Delay
from engine_animation import ONE_SHOT, LOOP, PING_PONG
from engine_animation import EASE_SINE_IN_OUT, EASE_ELAST_IN_OUT
```

## Tween — プロパティ補間アニメーション

`tween.start(target, property, from_value, to_value, duration_ms, intensity, mode, easing)`

| 引数 | 説明 |
|------|------|
| `target` | アニメーション対象のオブジェクト |
| `property` | プロパティ名（文字列）例: `"position"`, `"rotation"`, `"color"`, `"scale"` |
| `from_value` | 開始値 |
| `to_value` | 終了値 |
| `duration_ms` | 再生時間（ミリ秒） |
| `intensity` | 強度（通常 `1.0`） |
| `mode` | 再生モード（`ONE_SHOT` / `LOOP` / `PING_PONG`） |
| `easing` | イージング関数 |

`tween.after` にコールバック関数を設定するとアニメーション完了時に呼ばれる。

## 再生モード定数

| 定数 | 説明 |
|------|------|
| `ONE_SHOT` | 1回再生して終了 |
| `LOOP` | ループ再生 |
| `PING_PONG` | 往復再生 |

## イージング定数（主要なもの）

`EASE_SINE_IN_OUT`, `EASE_ELAST_IN_OUT`, `EASE_BACK_OUT` など

## 使用例

```python
from engine_animation import Tween, ONE_SHOT, EASE_ELAST_IN_OUT
from engine_nodes import Rectangle2DNode
import math

class MyRect(Rectangle2DNode):
    def __init__(self):
        super().__init__(self)
        self.tween = Tween()
        self.tween.after = self.on_done  # 完了コールバック

    def on_done(self, tween):
        print("アニメーション完了")

rect = MyRect()
rect.tween.start(rect, "rotation", 0.0, 2 * math.pi, 3000, 1.0, ONE_SHOT, EASE_ELAST_IN_OUT)
```
