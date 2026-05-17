# engine_physics — 物理演算

公式ドキュメント: https://color.thumby.us/doc/build/engine_physics.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_physics
```

| 関数/プロパティ | 説明 |
|----------------|------|
| `engine_physics.set_gravity(x, y)` | 重力ベクトルを設定（例: `set_gravity(0, -0.02)`） |
| `node.velocity` | `Vector2` で速度設定 |
| `node.gravity_scale` | `Vector2` で重力の影響倍率 |
| `node.dynamic` | `False` にすると静止オブジェクトになる |

物理ノード: `PhysicsRectangle2DNode`, `PhysicsCircle2DNode`（`engine_nodes.md` 参照）

衝突は `collision(self, contact)` をオーバーライドして検知する。

## 使用例

```python
import engine_main
import engine
import engine_physics
from engine_nodes import PhysicsRectangle2DNode, CameraNode
from engine_math import Vector2, Vector3

engine_physics.set_gravity(0, -0.02)

class Ball(PhysicsRectangle2DNode):
    def __init__(self):
        super().__init__(self)
        self.position = Vector2(0, 30)
        self.velocity = Vector2(1.0, 0)

    def collision(self, contact):
        self.velocity.y = abs(self.velocity.y)  # 床に当たったら上向きに跳ね返る

class Floor(PhysicsRectangle2DNode):
    def __init__(self):
        super().__init__(self)
        self.position = Vector2(0, -40)
        self.dynamic = False  # 静止オブジェクト

ball = Ball()
floor = Floor()
camera = CameraNode()
camera.position = Vector3(0, 0, 1)
engine.start()
```
