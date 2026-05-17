# engine_debug — デバッグ出力制御

公式ドキュメント: https://color.thumby.us/doc/build/engine_debug.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_debug
```

## 関数

| 関数 | 説明 |
|------|------|
| `engine_debug.enable_all()` | すべてのデバッグ出力を有効化 |
| `engine_debug.disable_all()` | すべてのデバッグ出力を無効化 |
| `engine_debug.enable_setting(setting)` | 指定レベルのみ有効化 |

## 定数

| 定数 | 値 | 説明 |
|------|-----|------|
| `engine_debug.info` | 0 | 情報レベル |
| `engine_debug.warnings` | 1 | 警告レベル |
| `engine_debug.errors` | 2 | エラーレベル |
| `engine_debug.performance` | 3 | パフォーマンス計測 |

## 使用例

```python
import engine_debug

engine_debug.enable_all()                              # 開発中：全出力有効
engine_debug.enable_setting(engine_debug.errors)       # エラーのみ表示
engine_debug.disable_all()                             # リリース時：全出力無効
```
