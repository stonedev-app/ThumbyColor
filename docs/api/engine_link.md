# engine_link — デバイス間通信

公式ドキュメント: https://color.thumby.us/doc/build/engine_link.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

2台のThumby Color間でシリアル通信によるデータ送受信を実現する。

```python
import engine_link
```

## メソッド

| メソッド | 説明 |
|---------|------|
| `engine_link.start()` | 通信開始（ホスト/クライアント自動判定） |
| `engine_link.stop()` | 通信停止 |
| `engine_link.connected()` | 接続状態を取得（bool） |
| `engine_link.is_host()` | ホスト側かどうかを確認（bool） |
| `engine_link.send(buffer, count=None, offset=0)` | データ送信（送信バイト数を返す） |
| `engine_link.read(count)` | 受信バッファからデータ読み出し（bytearray or None） |
| `engine_link.read_into(buffer, count, offset=0)` | 指定バッファへ読み込み（読込バイト数を返す） |
| `engine_link.available()` | 読み込み可能バイト数を取得 |
| `engine_link.clear_send()` | 送信バッファをクリア |
| `engine_link.clear_read()` | 受信バッファをクリア |
| `engine_link.set_connected_cb(callback)` | 接続時コールバック登録 |
| `engine_link.set_disconnected_cb(callback)` | 切断時コールバック登録 |

## 使用例

```python
import engine_link

def on_connected():
    engine_link.clear_send()
    engine_link.clear_read()

def on_disconnected():
    pass

engine_link.set_connected_cb(on_connected)
engine_link.set_disconnected_cb(on_disconnected)
engine_link.start()

# 送信
engine_link.send(b"Hello")

# 受信
if engine_link.available() > 0:
    data = engine_link.read(engine_link.available())
```
