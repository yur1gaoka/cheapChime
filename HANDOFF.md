# 引き継ぎメモ

## 概要

このプロジェクトは、ブラウザのみで動作するチャイム生成ツールです。  
実装は単一ファイルの `index.html` に集約されています。

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
- `index.html` をローカルでそのまま開いて動作

## 現在の主な機能

- 2点 / 3点 / 4点チャイム
- 10種類の音色プリセット
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
- 音量調整
- リバーブ量調整
- Low EQ / High EQ
- ループ再生
- WAV ダウンロード
- 再生パネルのドラッグ移動

## ファイル構成

- `index.html`
  - UI
  - スタイル
  - 音源ロジック
  - 再生
  - WAV 書き出し
- `README.md`
  - ユーザー向け説明
- `AGENTS.md`
  - 作業方針
- `HANDOFF.md`
  - この引き継ぎメモ
- `docs/`
  - 作業ルールと運用文書

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
  - コード、ボイス数、オクターブから発音計画を組み立て
- `scheduleVoice()`
  - 各音を生成
- `scheduleTransient()`
  - 立ち上がり成分を生成
- `renderChimeToContext()`
  - 再生と書き出し共通のレンダリング
- `downloadWav()`
  - `OfflineAudioContext` で WAV 出力
- `moveFloatingMeta()`
  - サマリーやステータスを再生パネルへ移動
- `initFloatingDrag()`
  - 再生パネルのドラッグ移動

## 現在の docs 運用

- 着手判断は `docs/project-profile.md` を基準にする
- 継続作業の状態管理は `docs/handover.md` を優先する
- `HANDOFF.md` は人間向けの概要メモとして残し、厳密な作業状態は `docs/` 側で管理する

## 確認時のポイント

1. ブラウザで `index.html` を開いて再生できるか
2. 音色プリセット切り替えが効くか
3. コード進行プリセットが正しく反映されるか
4. ボイス数変更が反映されるか
5. ループ再生が動くか
6. 再生パネルのドラッグ移動が効くか
7. WAV ダウンロードが動くか

## 残タスク・確認ポイント

- README と docs の記述差分は、今後の機能追加時に合わせて更新する
- 実機スマホでの挙動確認は未実施
- ライセンス表記の最終整理は未完了
- 音質調整時は既存プリセット差分と書き出し音の整合を要確認

## 継続開発の優先順位

1. 音質とプリセット差分の維持
2. ドキュメント整合の維持
3. UI 調整が必要な場合も、音源ロジックへの影響を優先確認
