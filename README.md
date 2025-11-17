
# Time Tracking Webアプリ企画書

---

## 1. 企画概要

**アプリ名（仮）：** AutoTimeTrack

**目的：**
Google Calendar と連携し、予定に基づいて自動で作業時間を計測・記録する Web アプリ。開発者やフリーランス、チーム向けに、作業時間の可視化と効率改善をサポートする。

**ターゲットユーザー：**
- システムエンジニア
- アプリ開発者
- フリーランス
- プロジェクトチーム

**特徴：**
- Google Calendar との自動同期
- タイトル・タグ・カレンダー名による自動分類
- ダッシュボードで作業時間を可視化
- 手動修正機能付き
- ポモドーロ等の手動タイマー不要

---

## 2. 背景・課題

- 既存のタイムトラッキングツールは手動操作が必要で記録の抜け漏れが発生しやすい
- Google Calendar の予定情報を自動で記録できるツールは少ない、もしくは有料
- チームやプロジェクト単位での時間集計や可視化が不十分

---

## 3. 主要機能

### 3.1 ユーザー認証
- Google OAuth 2.0 によるログイン
- Calendar API の認可

### 3.2 カレンダー同期
- カレンダー一覧取得・選択
- イベントの取得、変更・削除同期

### 3.3 自動計測ロジック
- カレンダー名によるフィルタ
- タイトル・Description タグによる自動分類
- 現在時間とイベントの開始/終了時間で稼働中を判断

### 3.4 タイムトラッキングデータ管理
- DB に保存（イベントごとにタイムエントリ生成）
- 日別・週別・カテゴリ別集計

### 3.5 ダッシュボード
- 今日/週の合計作業時間表示
- カテゴリ別グラフ表示
- イベント一覧表示

### 3.6 手動修正機能
- 自動記録された作業時間の編集
- 開始/終了時刻の上書き

---

## 4. 技術構成

| 層 | 技術 |
| --- | --- |
| フロントエンド | Next.js (React), Tailwind CSS |
| バックエンド | Next.js API Routes / Node.js + Express |
| DB | PostgreSQL + Prisma |
| 認証・API | Google OAuth 2.0, Google Calendar API |
| 可視化 | Chart.js / D3.js |
| デプロイ | Vercel / Supabase |

---

## 5. データ構造例

**users**: ユーザー情報 (id, google_id, name, email)

**calendars**: 追跡対象カレンダー (id, user_id, google_calendar_id, name, tracking_enabled)

**events**: 予定イベント (id, user_id, google_event_id, title, start, end, calendar_id, category, synced_at)

**time_entries**: 記録された作業時間 (id, user_id, event_id, start, end, category, source)

---

## 6. 開発ステップ

1. Google OAuth でログイン機能実装
2. Calendar API でイベント取得・同期
3. 自動分類ロジック実装
4. DB に記録、タイムエントリ生成
5. ダッシュボード画面作成（Chart.js等で可視化）
6. 手動修正機能追加
7. モバイル対応(PWA)・デプロイ

---

## 7. 差別化ポイント

- 完全自動で作業時間を記録（予定入力だけで記録される）
- 開発フェーズやカテゴリごとの分類が可能
- カレンダー変更に応じてログ自動更新
- 既存ツールよりも使いやすいUIとチーム対応機能

---

## 8. 画面モック概要

1. **Dashboard**: 今日・週の作業時間、カテゴリ別グラフ、時間推移チャート
2. **Calendar Sync**: カレンダー一覧と同期ON/OFF切替
3. **Auto Tracking Rules**: タイトル/タグ/カレンダー名で分類するルール設定
4. **Time Entries**: 自動・手動の作業時間ログ一覧

---

## 9. まとめ

AutoTimeTrackは、Google Calendar連携による自動計測と手軽な可視化を組み合わせ、開発者やチームの時間管理効率を飛躍的に向上させるWebアプリです。

