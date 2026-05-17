# engine_nodes — ノードクラス

公式ドキュメント: https://color.thumby.us/doc/build/engine_nodes.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
from engine_nodes import Sprite2DNode, CameraNode  # 必要なクラスをimport
```

ノードはサブクラス化して使うのが主流。`tick(self, dt)` をオーバーライドしてゲームループ処理を記述する。  
共通プロパティ: `position`, `rotation`, `scale`, `layer`, `opacity`, `visible`

`node.add_child(child)` で親子関係を構築（子は親の座標系に従う）。

| クラス | 用途 |
|--------|------|
| `CameraNode` | カメラ（必須）。`position=Vector3(x, y, 0)` で視点設定 |
| `Sprite2DNode` | 2Dスプライト描画 |
| `Text2DNode` | テキスト描画 |
| `Rectangle2DNode` | 矩形描画 |
| `Circle2DNode` | 円描画 |
| `Line2DNode` | 直線描画 |
| `PhysicsRectangle2DNode` | 矩形物理オブジェクト（`velocity`, `gravity_scale`, `dynamic` プロパティあり） |
| `PhysicsCircle2DNode` | 円形物理オブジェクト |
| `GUIButton2DNode` | GUIボタン（`on_just_pressed` 等のコールバックをオーバーライド） |
| `GUIBitmapButton2DNode` | 画像付きGUIボタン |
| `MeshNode` | 3Dメッシュ |
| `VoxelSpaceNode` | ボクセル空間 |
| `EmptyNode` | 空ノード（`add_child()` の親として使用） |

コンストラクタの引数詳細はオンラインドキュメントを参照。

## 使用例

```python
import engine_main
import engine
from engine_nodes import Sprite2DNode, CameraNode, EmptyNode
from engine_math import Vector2, Vector3
from engine_resources import TextureResource

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)
        self.texture = TextureResource("/Games/MyGame/player.bmp")
        self.position = Vector2(0, 0)

    def tick(self, dt):
        pass  # 毎フレーム処理

# 親子関係: root を親にして player をまとめる
root = EmptyNode()
player = Player()
root.add_child(player)

camera = CameraNode()
camera.position = Vector3(0, 0, 1)
engine.start()
```
