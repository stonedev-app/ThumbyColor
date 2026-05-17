# engine_math — 数学

公式ドキュメント: https://color.thumby.us/doc/build/engine_math.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
from engine_math import Vector2, Vector3
```

- `Vector2(x, y)` — 2D座標・サイズ・速度などに使う
- `Vector3(x, y, z)` — 3D座標（カメラ `position` 等）

## 使用例

```python
import engine_main
import engine
from engine_math import Vector2, Vector3
from engine_nodes import Sprite2DNode, CameraNode

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)
        self.position = Vector2(0, 0)
        self.velocity = Vector2(0, 0)

    def tick(self, dt):
        self.position.x += self.velocity.x * dt
        self.position.y += self.velocity.y * dt

camera = CameraNode()
camera.position = Vector3(0, 0, 1)
engine.start()
```
