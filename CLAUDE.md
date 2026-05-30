# Thumby Color 開発ガイド

## 概要

このディレクトリは Thumby Color 向けゲーム開発のルートです。
各ゲームプロジェクトはサブフォルダで管理します。

- **言語**: MicroPython
- **エンジン**: TinyCircuits Tiny Game Engine（C実装、MicroPythonバインディング）
- **公式ドキュメント**:
  - ドキュメント一覧: https://color.thumby.us/pages/documentation-and-examples/documentation-and-examples/
  - 各APIページ: `https://color.thumby.us/doc/build/{モジュール名}.html`
  - コード例（GitHub）: https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/tree/main/filesystem/Games

## デバイス仕様

| 項目 | 仕様 |
|------|------|
| CPU | RP2350 デュアルコア 150〜300MHz（FPU内蔵） |
| RAM | 520kB SRAM |
| Flash | 16MiB（ゲーム用 2MiB、ファイルシステム 13MiB） |
| 画面 | 0.85" 128×128px 16bit カラー TFT LCD |
| サウンド | 4kHz 磁気ブザー |
| 振動 | バイブレーションモーター |
| RTC | リアルタイムクロック内蔵（`engine_time` で日時取得） |
| バッテリー | 110mAh LiPo（約2時間） |
| サイズ | 51.6×30.0×11.6 mm |

### ボタン配置

| ボタン | `engine_io` 定数 |
|--------|-----------------|
| 十字キー上 | `btn.UP` |
| 十字キー下 | `btn.DOWN` |
| 十字キー左 | `btn.LEFT` |
| 十字キー右 | `btn.RIGHT` |
| Aボタン（右） | `btn.A` |
| Bボタン（右） | `btn.B` |
| 左ショルダー | `btn.LB` |
| 右ショルダー | `btn.RB` |
| メニュー | `btn.MENU` |

## 開発環境

### ブラウザエディタ
#### URL: https://color.thumby.us/code/
- 対応ブラウザ: Chrome / Edge のみ
- できること: コード編集 / エミュレータ動作確認 / 実機への直接転送/ REPL / ファイルシステム管理
- エミュレータ操作: W/A/S/D（十字キー）、`,`/`.`（A/Bボタン）、マウスクリック
- 実機転送: USB-C接続後、ファイルを右クリック → Upload to /Games

### Thonny
#### 公式サイト: https://thonny.org/
- できること: 実機へのファイル転送 / ファイルシステム管理 / REPLコンソール
- 初期設定: Tools > Options > Interpreter → MicroPython (Raspberry Pi Pico)
- 接続: USB-C接続後、赤い停止ボタンをクリック（「>>>」で接続完了）
- ファイル転送: View > Files → ファイルを右クリック → Upload to /Games

### mpremote
- できること: ファイル転送 / REPL / スクリプト実行（コマンドラインのみ・GUIなし）
- macOS ポート名: `/dev/tty.usbmodem*`
- 注意: Thonny と同時接続不可（シリアルポートの排他制御）

```bash
# デバイス一覧を確認
mpremote devs

# REPL を開く（終了: Ctrl-]）
mpremote repl

# ファイルをデバイスへアップロード（デバイス側パスに : プレフィックス必須）
mpremote cp main.py :/Games/ゲーム名/main.py

# デバイス上のファイル一覧
mpremote fs ls /Games/ゲーム名/

# スクリプトをデバイスRAM上で実行（書き込まずにテスト）
mpremote run main.py

# ディレクトリを再帰的にアップロード
mpremote fs cp -r ゲーム名/ :/Games/ゲーム名/
```

## プロジェクトのファイル構成

```
ThumbyColor/                        # このリポジトリのルート
  新規プロジェクト(ゲーム名)/          # 各ゲームのフォルダ
    main.py                         # エントリーポイント（必須・公式規定）
    icon.bmp                        # ランチャー用アイコン（任意）
    (リソースファイル等は自由に配置)
    .claude/
      settings.json                 # Stop hook（自動コードレビュー）
      commands/
        review.md                   # /review コマンド（手動コードレビュー）
  docs/
    api/                            # エンジン API リファレンス（13モジュール）
  .claude/
    commands/
      new-game.md                   # /new-game コマンド（新規プロジェクト作成）
  CLAUDE.md                         # このファイル
```

### 新規プロジェクト作成
ThumbyColor ルートで `/new-game ゲーム名` を実行すると自動作成される  

### 各プロジェクトフォルダについて
- 各プロジェクトフォルダに個別の`CLAUDE.md` を用意し、そのゲーム固有の情報を記載する  
- コードレビューは、各プロジェクトフォルダで `/review` を実行する
- Claudeによるソース修正は、自動でレビューされる

### ランチャーのゲーム認識規則
フォルダ内に以下のいずれかがあればゲームと認識される
- `main.py` — 標準エントリーポイント
- `manifest.ini` — エントリーポイントやアイコンを任意のファイル名で指定できる
- `icon.bmp` — 任意。なければランチャーで「?」アイコンになる。  
- `リソース(BMP等)の配置` - 規定なし。`textures/` 等のサブフォルダを作っても、直下に置いても自由。

## エンジン API

### APIリファレンス: `docs/api/{モジュール名}.md`（ThumbyColor/ルートからの相対パス）
- このAPIリファレンスは [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）時点の情報。
- 実機のファームウェア日付は `engine.firmware_date()` で確認できる。
- 内容が古い可能性がある場合は公式オンラインドキュメントを優先すること。

### 主要モジュール:
- [engine](docs/api/engine.md) — メインループ制御
- [engine_nodes](docs/api/engine_nodes.md) — ノードクラス
- [engine_io](docs/api/engine_io.md) — 入力・デバイス制御
- [engine_draw](docs/api/engine_draw.md) — 直接描画API
- [engine_resources](docs/api/engine_resources.md) — リソース管理
- [engine_math](docs/api/engine_math.md) — 数学
- [engine_save](docs/api/engine_save.md) — セーブデータ
- [engine_audio](docs/api/engine_audio.md) — サウンド
- [engine_physics](docs/api/engine_physics.md) — 物理演算
- [engine_animation](docs/api/engine_animation.md) — アニメーション（Tween）
- [engine_debug](docs/api/engine_debug.md) — デバッグ出力制御
- [engine_time](docs/api/engine_time.md) — RTC（日時）管理
- [engine_link](docs/api/engine_link.md) — デバイス間通信

### 基本パターン

**手続き型**（シンプルなゲーム向け）:
```python
import engine_main          # 必須・最初にimport
import engine
# ... 他のimport

# ノード・リソースの初期化

while True:
    if engine.tick():
        # ゲームロジック・描画
        pass
```

**クラス継承型**（実際のゲームで主流）:
```python
import engine_main
import engine
from engine_nodes import Sprite2DNode, CameraNode

class Player(Sprite2DNode):
    def __init__(self):
        super().__init__(self)

    def tick(self, dt):             # 毎フレーム呼ばれる
        pass

    def collision(self, contact):   # 衝突コールバック（物理ノードのみ）
        pass

player = Player()
camera = CameraNode()
engine.start()
```

`node.add_child(child)` で親子関係を構築（子は親の座標系に従う）。

## コーディング規約

- **型ヒントは使わない**（MicroPythonは `# type: ignore` でLinterを抑制）
- **`import engine_main` は必ず最初**にimportする
- グローバル変数を関数内で書き換えるときは `global` 宣言を忘れずに
- リソースファイル（画像・サウンド・フォント等）のパスはデバイス上の絶対パスで書く（例: `/Games/ゲーム名/textures/img.bmp`）
- FPSは基本 `30` に設定（`engine.fps_limit(30)`）
- `framebuf` を使う場合、`engine_draw.front_fb()` でフロントバッファを取得する

## 各プロジェクトのCLAUDE.md に書くべき内容

```markdown
# [ゲーム名]

## ゲーム概要
（どんなゲームか、ジャンル、操作方法）

## デバイス上のパス
/Games/[ゲーム名]/

## ファイル構成
（プロジェクト固有のファイル・フォルダ説明）

## 実装メモ
（特有のアルゴリズム、既知の制約、TODO等）

## コマンド
- `/review` — コードレビューを手動実行
```
