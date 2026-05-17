# engine_audio — サウンド

公式ドキュメント: https://color.thumby.us/doc/build/engine_audio.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_audio
```

| 関数 | 説明 |
|------|------|
| `engine_audio.set_volume(level)` | 音量設定（0.0〜10.0 程度） |
| `engine_audio.play(sound, channel, loop)` | 再生（channel: 0〜3、loop: True/False） |

リソースの種類は `engine_resources.md` を参照。

## 使用例

```python
import engine_main
import engine
import engine_audio
import engine_io as btn
from engine_resources import WaveSoundResource, ToneSoundResource
from engine_nodes import Sprite2DNode

bgm = WaveSoundResource("/Games/MyGame/bgm.wav")
beep = ToneSoundResource()
beep.frequency = 880

engine_audio.set_volume(5.0)
engine_audio.play(bgm, 0, True)  # チャンネル0でBGMをループ再生

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)

    def tick(self, dt):
        if btn.A.is_just_pressed:
            engine_audio.play(beep, 1, False)  # チャンネル1で効果音
```
