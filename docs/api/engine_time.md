# engine_time — RTC（日時）管理

公式ドキュメント: https://color.thumby.us/doc/build/engine_time.html

> 参照: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

```python
import engine_time
```

## 関数

### `engine_time.datetime(time=None)`

引数なしで現在の日時を取得、タプルを渡すと日時を設定する。

- **取得時の戻り値**: `(year, month, mday, hour, min, sec, wday, yday)`
- **設定時の入力**: `(year, month, day, hour, minute, second)`
- **設定時の戻り値**: `RTC_OK` または `RTC_I2C_ERROR`

### `engine_time.is_compromised()`

RTCの時刻整合性を確認。`True` なら時刻が不正。

## 定数

| 定数 | 説明 |
|------|------|
| `engine_time.RTC_OK` | RTC操作成功 |
| `engine_time.RTC_I2C_ERROR` | I2C通信エラー |

## 使用例

```python
import engine_time

# 現在時刻を取得
year, month, day, hour, minute, second, wday, yday = engine_time.datetime()

# 日時を設定
status = engine_time.datetime((2024, 7, 24, 11, 49, 0))
if status == engine_time.RTC_OK:
    print("設定成功")

# 整合性チェック
if engine_time.is_compromised():
    print("時刻が不正")
```
