# 引き継ぎメモ

## 概要

このプロジェクトは、ブラウザのみで動作するチャイム生成ツールです。  
実装は単一ファイルの [`index.html`](/K:/chime/index.html) に集約されています。

技術構成:

- HTML
- CSS
- JavaScript
- Web Audio API
- OfflineAudioContext

制約:

- 外部ライブラリなし
- CDN なし
- サーバ不要
- ローカルでそのまま開いて動作

## 現在の主な機能

- 2点 / 3点 / 4点チャイム
- 複数の音色プリセット
  - Standard Bell
  - Soft Chime
  - Bright Synth Chime
  - Aircraft Cabin
  - Music Box
  - Crystal Guide
  - Velvet Pad Chime
  - Warm EP
  - Guide Organ
  - Analog Pad
- コード進行プリセット
  - デフォルト
  - あいさつ
  - 飛行場
  - カノン
  - 王道
  - 小室
- 各ステップごとのコード選択
- 各ステップごとのオクターブ選択
- 一括オクターブ変更
- 単音 / 2ボイス / 3ボイス / 4ボイス
- ピッチ調整
- テンポ調整
  - UI 上は BPM 表示
  - スライダーは右ほど速い
- 音量調整
- リバーブ量調整
- Low EQ / High EQ
- ループ再生
- WAV ダウンロード
- 再生パネルのドラッグ移動

## ファイル構成

- [`index.html`](/K:/chime/index.html)
  - UI
  - スタイル
  - 音源ロジック
  - 再生
  - WAV 書き出し
- [`README.md`](/K:/chime/README.md)
  - ユーザー向け説明
- [`AGENTS.md`](/K:/chime/AGENTS.md)
  - 作業方針
- [`HANDOFF.md`](/K:/chime/HANDOFF.md)
  - この引き継ぎメモ

## 実装上の要点

### 音源

- プリセット定義は `PRESETS`
- チャイム点数定義は `PATTERNS`
- コード定義は `CHORD_LIBRARY`
- コード進行プリセットは `PROGRESSION_PRESETS`

### 主要関数

- `getSettings()`
  - UI から現在値を取得
- `updateUi()`
  - 表示更新
- `buildNotePlan()`
  - コードとボイス数から発音計画を組み立て
- `scheduleVoice()`
  - 各音を生成
- `renderChimeToContext()`
  - 再生と書き出し共通のレンダリング
- `downloadWav()`
  - OfflineAudioContext で WAV 出力
- `moveFloatingMeta()`
  - サマリーやステータスを再生パネルへ移動
- `initFloatingDrag()`
  - 再生パネルのドラッグ移動

## 最近のUI方針

- 右ペインのサマリーは独立表示をやめ、再生パネル側へ統合
- ステータスは大きく見せず、再生パネル内の補助情報として扱う
- スライダー部は英語ラベルのみ
- 補助説明文は減らしてシンプル化

## 移行時の注意

1. このフォルダは Git 管理下ではありません
2. 移行先の Git リポジトリへは、まず `index.html` を最優先で持っていけば動作を再開できます
3. ドキュメントも引き継ぐなら `README.md` `AGENTS.md` `HANDOFF.md` を一緒に移してください
4. 単一ファイル要件を崩さない前提で開発が進んでいます

## 移行先で最初に確認すべきこと

1. ブラウザで `index.html` を開いて再生できるか
2. 音色プリセット切り替えが効くか
3. コード進行プリセットが正しく反映されるか
4. ループ再生が動くか
5. 再生パネルのドラッグ移動が効くか
6. WAV ダウンロードが動くか

## 残タスク・確認ポイント

- UI は最後にかなり調整しているため、再生パネルまわりは実ブラウザで見た目確認推奨
- 最近の変更で再生パネルへ要素を移動しているため、レイアウト崩れがないか要確認
- スライダー表記は英語へ寄せたが、他 UI は日本語中心のまま
- 必要なら移行先で文言統一を行う

## 継続開発の優先順位

1. レイアウトの安定化
2. 音色の整理
3. プリセットの微調整
4. UI 文言の統一
5. Git リポジトリ側で履歴管理を開始

