# Thumby Color 開発環境

![言語](https://img.shields.io/badge/言語-MicroPython-blue)
![デバイス](https://img.shields.io/badge/デバイス-Thumby%20Color-orange)
![AI](https://img.shields.io/badge/AI-Claude%20Code-blueviolet)

## 概要

[Thumby Color](https://color.thumby.us/) 向けゲーム開発のルートリポジトリです。  
Claude Code を使った開発を想定した環境設定・ドキュメントを管理します。

> **注意**: このリポジトリにゲーム本体は含まれません。各ゲームプロジェクトはフォルダごとに独立した git リポジトリで管理します。

## このリポジトリに含まれるもの

| パス | 内容 |
|------|------|
| `CLAUDE.md` | Claude Code 向け AI 開発ガイド |
| `docs/api/` | エンジン API リファレンス（13モジュール） |
| `.claude/commands/new-game.md` | `/new-game` コマンド（新規プロジェクト作成） |

## 前提

- Thumby Color 実機、または[公式ブラウザエミュレータ](https://color.thumby.us/code/)（Chrome / Edge）
- Claude Code

## 使い方

### 新規ゲームプロジェクトを作成する

ThumbyColor ルートで Claude Code を開き、以下を実行します。

```
/new-game ゲーム名
```

以下のファイルが自動生成されます。

```
ゲーム名/
  main.py                        # ボイラープレート
  CLAUDE.md                      # プロジェクト情報テンプレート
  .claude/
    settings.json                # Stop hook（自動コードレビュー）
    commands/
      review.md                  # /review コマンド（手動コードレビュー）
```

### コードレビュー

| 方法 | タイミング |
|------|-----------|
| **自動**（Stop hook） | Claude による作業終了時に自動実行 |
| **手動**（`/review`） | 各ゲームフォルダで任意のタイミングに実行 |

コードレビューは `CLAUDE.md` のコーディング規約に基づいてサブエージェントが行います。

## API リファレンス

`docs/api/` 配下に以下の13モジュールのリファレンスがあります。

| モジュール | 概要 |
|-----------|------|
| `engine` | メインループ制御 |
| `engine_nodes` | ノードクラス |
| `engine_io` | 入力・デバイス制御 |
| `engine_draw` | 直接描画API |
| `engine_resources` | リソース管理 |
| `engine_math` | 数学 |
| `engine_save` | セーブデータ |
| `engine_audio` | サウンド |
| `engine_physics` | 物理演算 |
| `engine_animation` | アニメーション（Tween） |
| `engine_debug` | デバッグ出力制御 |
| `engine_time` | RTC（日時）管理 |
| `engine_link` | デバイス間通信 |

> エンジンバージョン: [TinyCircuits/TinyCircuits-Tiny-Game-Engine](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine) `main` @ [`8f75dc9`](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/commit/8f75dc9)（2026-03-13）

## 各ゲームプロジェクトについて

各ゲームプロジェクトはこのリポジトリでは管理しません。  
プロジェクトフォルダごとに `git init` して独立したリポジトリとして管理します。

## 参考リンク

- [Thumby Color 公式ドキュメント](https://color.thumby.us/pages/documentation-and-examples/documentation-and-examples/)
- [エンジンコード例（GitHub）](https://github.com/TinyCircuits/TinyCircuits-Tiny-Game-Engine/tree/main/filesystem/Games)
- [Thonny](https://thonny.org/)（実機へのファイル転送ツール）
