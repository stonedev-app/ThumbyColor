# engine_save — セーブデータ

公式ドキュメント: https://color.thumby.us/doc/build/engine_save.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_save
```

| 関数 | 説明 |
|------|------|
| `engine_save.set_location("save.data")` | 保存ファイルのパスを指定（ゲーム起動時に1回呼ぶ） |
| `engine_save.save("key", value)` | 値を保存 |
| `engine_save.load("key", default)` | 値を読み込み（キーがなければ `default` を返す） |
| `engine_save.delete("key")` | キーを削除 |

対応型: 文字列、数値、`Vector2`, `Vector3`, `Color`, `bytearray`

## 使用例

```python
import engine_save

engine_save.set_location("save.data")  # ゲーム起動時に1回呼ぶ

# 読み込み（初回はデフォルト値の 0 が返る）
high_score = engine_save.load("high_score", 0)

# ゲーム終了時に更新
current_score = 1500
if current_score > high_score:
    engine_save.save("high_score", current_score)
```
