# engine — メインループ制御

公式ドキュメント: https://color.thumby.us/doc/build/engine.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_main  # 必須・最初にimport
import engine
```

| 関数 | 説明 |
|------|------|
| `engine.tick()` | 1フレーム処理、描画タイミングで `True` を返す |
| `engine.start()` | シンプルな無限ループ開始（tick不要） |
| `engine.end()` | エンジン停止 |
| `engine.fps_limit(fps)` | FPS上限を設定（例: `engine.fps_limit(30)`） |
| `engine.dt()` | 前フレームからの経過時間を取得（秒）。最初のフレームは 0.0 |
| `engine.get_running_fps()` | 実際のFPSを取得 |
| `engine.reset(soft_reset)` | エンジンリセット |
| `engine.freq(hz)` | CPU周波数設定 |

## 使用例

```python
import engine_main
import engine

engine.fps_limit(30)

# tick型: 手続き型スタイル
while True:
    if engine.tick():
        dt = engine.dt()  # 前フレームからの経過時間（秒）
        # speed * dt で移動量を計算すると、処理落ち時もスローモーションにならない
```

クラス継承型では `engine.start()` を使う（`engine_nodes.md` 参照）。
