# engine_resources — リソース管理

公式ドキュメント: https://color.thumby.us/doc/build/engine_resources.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
from engine_resources import TextureResource, FontResource
from engine_resources import ToneSoundResource, WaveSoundResource, RTTTLSoundResource
```

| クラス | 使い方 |
|--------|--------|
| `TextureResource("path.bmp")` | BMPファイルを読み込み |
| `TextureResource(w, h, color, bpp)` | 空テクスチャ作成（描画バッファ用） |
| `FontResource("font.bmp")` | フォントBMPを読み込み |
| `ToneSoundResource()` | 単音（`.frequency` プロパティで音程変更） |
| `WaveSoundResource("file.wav")` | WAVファイル |
| `RTTTLSoundResource("file.rtttl")` | RTTTL形式（着信音形式） |

## 使用例

```python
import engine_main
import engine
import engine_audio
from engine_resources import TextureResource, FontResource, ToneSoundResource
from engine_nodes import Sprite2DNode

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)
        self.texture = TextureResource("/Games/MyGame/player.bmp")

font = FontResource("/Games/MyGame/font.bmp")

beep = ToneSoundResource()
beep.frequency = 440  # A4（ラ）
engine_audio.play(beep, 0, False)
```
