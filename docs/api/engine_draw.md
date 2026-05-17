# engine_draw — 直接描画API

公式ドキュメント: https://color.thumby.us/doc/build/engine_draw.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_draw
from engine_draw import Color
```

| 関数 | 説明 |
|------|------|
| `engine_draw.rect(color, x, y, w, h, outline, opacity)` | 矩形 |
| `engine_draw.circle(color, cx, cy, r, outline, opacity)` | 円 |
| `engine_draw.line(color, x1, y1, x2, y2, opacity)` | 直線 |
| `engine_draw.pixel(color, x, y, opacity)` | ピクセル |
| `engine_draw.text(font, text, blend_color, x, y, ls, lh, opacity)` | テキスト |
| `engine_draw.blit(texture, x, y, transparent_color, opacity)` | テクスチャ描画 |
| `engine_draw.clear(color)` | 画面クリア |
| `engine_draw.front_fb()` | フロントバッファ（framebuf互換） |
| `engine_draw.back_fb()` | バックバッファ（framebuf互換） |
| `engine_draw.set_background(texture)` | 背景テクスチャ設定 |

`Color(r, g, b)` — 各成分 0〜255

色定数: `black`, `white`, `red`, `green`, `blue`, `yellow`, `cyan`, `magenta`, `orange`, `pink`, `navy`, `purple`, `gold`, `silver`, `skyblue` など（詳細はオンラインドキュメント参照）

## 使用例

```python
import engine_main
import engine
import engine_draw
from engine_draw import Color
from engine_resources import FontResource

font = FontResource("/Games/MyGame/font.bmp")
RED = Color(255, 0, 0)

engine.fps_limit(30)

while True:
    if engine.tick():
        engine_draw.clear(engine_draw.black)
        engine_draw.rect(RED, 10, 10, 40, 20, False, 1.0)
        engine_draw.circle(engine_draw.blue, 64, 64, 15, True, 1.0)
        engine_draw.text(font, "SCORE:100", engine_draw.white, 4, 4, 0, 0, 1.0)
```
