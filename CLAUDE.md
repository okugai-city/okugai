# fx-salon — 億街サロン（本番稼働中・最重要プロジェクト）

FX投資コミュニティ「億街サロン」の公開サイト一式＋会員基盤。**本番ドメイン okugai.net で稼働中**。
世界観=「億り人が住む電脳の街」。開街 2026-08-08(土)。決済は2026-08-03からテレコムクレジットで本番稼働。

## ⚠️ 最重要: push＝本番デプロイ

Cloudflare Pagesが `git push origin main` で**自動的に本番反映**する。push前に必ず社長確認。
gitignoreされた事業md（PLAN/REQUIREMENTS/DESIGN/STORY/CHARACTERS等13本）と `backend/` `docs/` は**非公開ローカル管理＝絶対にコミットしない**。

## 構成

- `hp/` 億街ポータル（世界観） / `lp/` 移住案内=セールス＋法務3点（tokushoho/privacy/kiyaku）
- `media/` 展望塔=コラム41本＋業者レビュー33本＋比較（アフィ収益面、`aff-links.js`）
- `room/` 会員マイページ / `admin/` 運営CRM（両方robots Disallow） / `join/` 入居受付（決済ページ） / `welcome/` 決済後→Discord連携
- `data/` サイトが読むJSON（news.json等） / `en/`系 英語版（**日英ペアで保守**）
- `backend/supabase/functions/` 本番Edge Function 8本（telecom-webhook / line-webhook / discord-interactions / morning-news 等）
- Supabase本番: project `xtrtbgymwsexzadrjedg`

## 触ると危険なもの

- **法務ページ（lp/tokushoho・privacy・kiyaku＋en版）**: テレコムクレジットの審査対象。文言変更は社長決裁必須
- **決済まわり**: 現行決済は**テレコム**（telecom-webhook Edge Function）。`functions/api/stripe-webhook.js` と旧Stripe記述はStripe閉鎖(2026-07-28)後の遺物＝復活させない。lp/index.htmlの旧Stripeリンクは死んでいる（導線は/join/）
- **`backend/supabase/functions/morning-news/deploy.sh` は実行厳禁**（APIキー対話入力でSecretsを上書き＋デプロイする）
- `tools/set-address.sh`（特商法の実住所）/ `tools/restore-affiliate-pages.sh`（git revertを伴う）は社長確認なしに実行しない

## コンプラ・文言の掟（金商法・景表法）

- **シグナル配信・売買推奨・「先出し」表現は全チャネル絶対NG**（無登録投資助言業の典型摘発パターン）。同じ機能は「リアルタイム公開」「観戦して学ぶ」で表現する
- 成果保証・月利/勝率の売り文句NG。実績は記録簿の事実開示のみ
- **オファーの正典=本番 `lp/index.html`**。現行: 2026年9月末まで移住費¥0、10月から¥9,800/月・縛りなし。旧表記（先着50名/半額4,900円/3ヶ月縛り）の混入は事故
- キャラ口調は `CHARACTERS.md`（非公開）が正。大家=フレンドリー、住人は「です・ます」
- 生成文には [가-힯Ѐ-ӿ] スキャン必須（ハングル/キリル混入が頻発した経緯あり）

## 作業の型

- **モバイル対応は必ずSkill `okugai-mobile-design` に従う**（縮小でなく600px以下専用設計ブロック。~/.claude/skills/に格納済み）
- 国内/海外の比較ページは**構造ごと完全対称**を保つ（片側だけの変更NG・2度指摘済み）
- 街に大きな変更（コラム公開/募集開始/施設オープン）を加えたら `data/news.json` にも追記する
- デザインは「本物のデータで見せる」。モック/サンプルUIの提案は原則しない
- 事業判断の前に `DESIGN.md`（動線の正典）と `ROLES.md`（機能の一枚地図——新しい建物を足す前に必ずここ）を読む

## 記憶・関連（作業後はここに書き戻す）

- サイト・事業の経緯: `~/.claude/projects/-Users-kenya/memory/fx-salon-project.md`
- 決済の経緯・監視: `~/.claude/projects/-Users-kenya/memory/okugai-payment-gateway-status.md`
- LINE/Discord自動応答: `~/ai-funnel`（億街LINEはSupabase line-webhookに一本化済み・2026-07-26）
- Bot類: `~/okugai-bot/`（棚卸しバッチ等launchd） / 審査書類: `~/okugai-shinsa/`（機微・外部送信禁止）
