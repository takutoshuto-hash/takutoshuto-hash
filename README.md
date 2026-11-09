# 首藤卓登 (Takuto Shuto)

**現場の業務を聞いて、システムと生成AIを自分で作り、毎日使われるところまで持っていくエンジニア**

[![Zenn](https://img.shields.io/badge/Zenn-@takutoshuto-3EA8FF?logo=zenn&logoColor=white)](https://zenn.dev/takutoshuto)
[![Live Demo](https://img.shields.io/badge/Live_Demo-GiftDesk-2EA44F?logo=googlechrome&logoColor=white)](https://takutoshuto-hash.github.io/gift-order-demo/)
[![CI mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/mail-triage-agent/actions)
[![CI social-post-agent](https://github.com/takutoshuto-hash/social-post-agent/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/social-post-agent/actions)
[![CI unified-order-model](https://github.com/takutoshuto-hash/unified-order-model/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/unified-order-model/actions)

専門の開発部署がない食品・ホスピタリティ系の会社で、EC・Webマーケティングと社内システム開発を一人で兼任しています。入社したとき、受注は **FAX と Excel だけ**でした。効率化のために受注・出荷のシステムを作り、Amazon やカタログギフトの Web 申込など事業の入口が増えるたびに作り足した結果、システムは **4つ（GAS 3本・PHP 1本）** に分かれました。そこで 2026年9月に **1つの注文モデルにまとめ直し**、PHP + MySQL の自社アプリ（61テーブル・約7万行）として、旧システムを止めずに段階的に本番へ移しました。社内3名が毎日使うため、楽観ロック・採番の原子化・冪等な取り込みで、**同時に使ってもデータが壊れない**作りにしています。

生成AI（Claude / Gemini）は「**AIが下書きし、人が確定する**」前提で本番に入れています。FAX注文書の構造化抽出、19施設の口コミ返信、SNS投稿案のAIエージェントがそれです。実装は Claude Code と組んで進め、設計・レビュー・テスト・本番への反映は自分で持ちます。

---

## 📦 まず見てほしい公開コード

実務で動いているものを、固有情報をダミーに置き換えて公開しています。**テストと CI 付き**で、外部APIに接続せずに `pytest` / `vitest` が通ります。

| リポジトリ | 何か | 技術 | テスト / CI |
|---|---|---|---|
| **[unified-order-model](https://github.com/takutoshuto-hash/unified-order-model)** | 4つの受注システムでバラバラだった「注文」を1つのモデルにそろえる変換。依頼主がいない注文・空のお届け先・旧システムのステータスを型で止める（本番 PHP の設計を TypeScript で表し直したもの） | TypeScript（strict） / Vitest | Vitest 46ケース（型のテストを含む）・GitHub Actions（Node 20〜24）・[解説記事](https://zenn.dev/takutoshuto/articles/1485430c919762) |
| **[social-post-agent](https://github.com/takutoshuto-hash/social-post-agent)** | Slackの一言から Notion の事実を参照して Instagram 投稿案を月10件生成するAIエージェント（本番稼働中のものの公開版） | Python / AWS Lambda・DynamoDB・EventBridge・SAM / Claude / Gemini | pytest 41ケース・GitHub Actions |
| **[mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent)** | 毎朝の受信メールを重要度で仕分けし、重要なものだけ Slack に届けるAIエージェント。返信は下書きまで（人が送る） | Python / AWS SAM / Claude / Gemini / IMAP | pytest 57ケース・GitHub Actions（3.11〜3.13） |
| **[gift-order-demo](https://github.com/takutoshuto-hash/gift-order-demo)** | 受注管理SPA「GiftDesk」の公開デモ。入力1回で送り状CSV・指示書・熨斗・月次集計まで | HTML / CSS / Vanilla JS（単一ファイル） | [ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **OCR Trust Agent** | 手書きFAX注文書を Gemini で読み、根拠のある項目だけ自動確定し、人の修正から学んで要確認を減らすエージェント（Agentic AI Hackathon with Google Cloud vol.5 応募作・**一次審査通過**） | Python / Gemini / ADK / Cloud Run / Cloud Scheduler | pytest 240ケース超。結果発表まで非公開（面接時に画面共有できます）・[概要記事](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33) |

2つのエージェントは共通の「契約駆動（agents as tools）」基盤の上に作っていて、Human-in-the-loop・冪等・コストガードレールの考え方をそろえています。

---

## 🔑 実績ハイライト

- 📦 **受注・出荷のシステムを4つゼロから作り、1つの注文モデルに統合して PHP + MySQL の自社アプリとして本番移行**（稼働中）— 「注文 → お届け先 → 明細」の3段・61テーブル。9つの受注チャネルをアダプタで共通の形にし、入金確認（銀行CSV照合）〜送り状CSV〜出荷指示書〜追跡番号取込〜発送完了メールを1画面に。旧システムは止めずに入口ごとのスイッチで切り替え。753コミット・PR 約130（2026年9〜11月）（[全体の流れ](https://zenn.dev/takutoshuto/articles/12562ee33ede1e)・[設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)）
- 🔒 **3人が同時に使ってもデータが壊れない作り** — 版番号による楽観ロック・採番の原子化（デッドロックを直した）・名前付きロック・冪等な取り込み・二重送信の防止。古いシステムに残る記録と新しい台帳を1時間ごとに突き合わせる見張りも入れた
- 🎁 **受注・出荷の業務システムを内製** — FAX手書き注文のOCR取り込みから、送り状CSV・出荷指示書・熨斗・請求まで1画面に統合。繁忙期は **月1,000〜2,000件** を処理
- 📮 **はがきだけだったカタログギフトの申込に Web 申込を提案・追加** — QR から申込番号をその場で照合。**Web申込 約7割**（88/127件）、**入力ミス 約5% → 0.5%未満**
- 🗺️ **Googleマップ（GBP）運用を19施設ぶん内製化** — 業者見積で **年 約565万円相当を ¥0** 運用。滞留していた口コミ **約6,000件を3ヶ月で返信**し、返信率を実質100%へ
- 📈 **多店舗チェーンのSEOを半自動化** — ブログ経由の **検索クリックを約8.3倍**（132 → 1,093回）に（GA4 / Search Console × 生成AI）
- 🤖 **AWSサーバーレス × Claude でAIエージェント** — 契約駆動 / Human-in-the-loop / 多層コストガードレールで、設計から約3週間で本番稼働

---

## 🛠 代表プロジェクト

| プロジェクト | 概要 | 主な技術 | リンク |
|---|---|---|---|
| **受注・出荷の統合（統一注文モデル）** | 自社EC・直送ギフト・カタログギフト・Amazon・はがき/FAXの注文を1つのモデルに正規化し、出荷業務を1画面化。本番移行済み | PHP / MySQL / PDO / React・TypeScript / ヤマトB2 CSV | [全体の流れ](https://zenn.dev/takutoshuto/articles/12562ee33ede1e)・[設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)・[PHP出荷支援の記事](https://zenn.dev/takutoshuto/articles/ae8ed60e00a0ca)・[型で表し直したコード](https://github.com/takutoshuto-hash/unified-order-model) |
| **GiftDesk（受注管理）** | 申込入力から送り状CSV・指示書・熨斗・請求書までを1つのSPAに統合。FAX注文書はLLMで構造化抽出 | Google Apps Script / スプレッドシート / Gemini API | [解説記事](https://zenn.dev/takutoshuto/articles/bc2ff859475742)・[ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **カタログギフト Web申込＋受注管理** | はがき OCR・QR 照合の Web 申込・送り状CSV・Amazon 取込まで、受付〜出荷を1つのアプリに | Google Apps Script / GitHub Pages / Gemini API | — |
| **手書き帳票のLLM×OCR** | 自作OCRで挫折し、Cloud Vision → Gemini にたどり着くまで。ハッカソンでは「信頼が育つ」エージェントへ発展 | Gemini API / Cloud Vision / Python | [解説記事](https://zenn.dev/takutoshuto/articles/a9e73fa4ed60ca)・[エージェント版](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33) |
| **GBP/MEO 内製化** | 19施設の口コミ返信（AI下書き＋一括投稿）・数値監視・営業時間の改ざん検知・月次レポートを自作 | Python / Google Business Profile API / BigQuery / Looker Studio / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/b589f1516c5052) |
| **多店舗SEO分析** | 制作会社任せだったGA4/GSCを自社に取り戻し、月次レポート＋ブログ運用を半自動化 | GA4 / Search Console / Python / BigQuery / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/850997ad982ff4) |
| **AX Marketing Hub** | Slackの自然文から Notion の事実を参照し、Instagram投稿案を月10件まとめて生成するAIエージェント | Python / AWS(Lambda・DynamoDB・EventBridge・SAM) / Claude / Notion / Slack | [解説記事](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)・[コード](https://github.com/takutoshuto-hash/social-post-agent) |
| **メール整理エージェント** | 受信メールを自動で仕分け・要約・ラベリングし、機械が下書き・人が確定する運用に | Python / AWS SAM / Claude | [コード](https://github.com/takutoshuto-hash/mail-triage-agent) |

---

## 🧪 個人開発・挑戦

- **OCR Trust Agent**（Agentic AI Hackathon with Google Cloud vol.5・**一次審査通過**）— 手書きFAX注文書を Gemini で読み、根拠のある項目だけ自動で確定し、人の修正から学んで確認の手間を減らすエージェント。14日間のシミュレーションで **要確認率 51% → 14%**、自動確定の誤り 0.29%。テスト240ケース超（Python / Gemini / ADK / Cloud Run）。[概要記事](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33)
- **AtCoder Heuristic Contest 074**（初参加・With AI 部門）— **532人中237位**。最適化問題で、最初の解から評価値を54%改善
- **WooCommerce 用プラグイン**（個人開発）— 日本のギフト・食品ネットショップ向けの日本式チェックアウト（ふりがな・郵便番号からの住所補完・のし・お届け日時の指定）。WordPress.org のレビューを通過して公開（PHP / WooCommerce）

---

## ✍️ 書いたもの（Zenn）

実務で作ったシステムの設計判断と落とし穴を記事にしています。→ **[zenn.dev/takutoshuto](https://zenn.dev/takutoshuto)**

- [FAXとExcelだけの受注業務に、システムを作り、増え、1つにまとめるまで — 食品ギフト会社の1年](https://zenn.dev/takutoshuto/articles/12562ee33ede1e)
- [4つの受注システムの「注文」を、TypeScript の型で1つにする — null・空配列・ステータスを型で止める](https://zenn.dev/takutoshuto/articles/1485430c919762)
- [ECの管理画面を我慢せず"横"に作る — Welcart自社ECの入金確認〜発送メールを1画面に、PHP×Claude Codeで](https://zenn.dev/takutoshuto/articles/ae8ed60e00a0ca)
- [「注文」という言葉が、4つのシステムで4つの意味を持っていた — バラバラな受注を"1つの注文モデル"に統合した設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)
- [信頼が育つOCR AI エージェント ― 手書き FAX 注文書の確認を「全部」から「例外」へ](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33)
- [手書きFAX・ハガキ注文をLLM×OCRで構造化する — 自作OCRで挫折し、Vision→Geminiにたどり着くまで](https://zenn.dev/takutoshuto/articles/a9e73fa4ed60ca)
- [FAXの手書き注文を、GASとスプレッドシートだけで「送り状CSV〜請求書まで一気通貫」にした話（IT予算ゼロの業務効率化）](https://zenn.dev/takutoshuto/articles/bc2ff859475742)
- [業者見積 年565万円のGoogleマップ運用（19施設）を¥0で内製し、溜まっていた約6,000件の口コミ返信を3ヶ月で片付けた](https://zenn.dev/takutoshuto/articles/b589f1516c5052)
- [制作会社任せだったアクセス解析を自社に取り戻し、月30分レポート＋週1本のSEOブログ運用にしたら検索クリックが8倍になった](https://zenn.dev/takutoshuto/articles/850997ad982ff4)
- [Slackに一言で企業Instagramの投稿案が10件出る仕組みを、AWSサーバーレス×Claudeで作った](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)

---

## 🧰 技術スタック

- **言語**：Python / JavaScript・TypeScript（Google Apps Script・React）/ PHP / SQL / HTML・CSS
- **LLM・AI**：Anthropic API（Claude／Tool use・プロンプトキャッシュ・モデルの使い分け・構造化出力）/ Gemini API（マルチモーダル）/ Google ADK / Google Cloud Vision API
- **クラウド・データ**：AWS（Lambda・DynamoDB・EventBridge・SAM・S3）/ Google Cloud（Cloud Run・Cloud Functions・Scheduler・Cloud Storage）/ BigQuery / Looker Studio / MySQL
- **開発の作法**：Git・GitHub（PR単位）/ pytest・Vitest（外部APIはモック）/ GitHub Actions / IaC（AWS SAM・Dockerfile）/ Claude Code との協働開発（設計・レビュー・本番確認は自分）
- **連携・公開**：Slack API / Notion API / Google Business Profile API / ヤマトB2クラウド / Welcart・WordPress / GitHub Pages / Chrome拡張

---

## 💡 設計で大事にしていること

- **機械が下書き、人が承認（Human-in-the-loop）** — OCR・AI返信・入金/発送など、公開・課金・誤配送が絡む操作は必ず人が最終判断
- **制約が設計を強くする** — IT予算ゼロ・非IT人材が毎日使う、という制約を前提に「小さく作って価値を出す」
- **同時に使っても壊れない** — 版番号の楽観ロック・採番の原子化・名前付きロック・冪等な取り込みで、二重実行や取り違えを防ぐ
- **壊れにくく作る** — 列は名前で引く（位置を固定しない）・型を守る（先頭ゼロや長い伝票番号は文字列）
- **取り消せない操作は3点セット** — 確認画面・ログ・取り消しを最初から入れる（メール送信・ステータス変更）
- **agents as tools（契約駆動）** — 生成AIを組む時は共通の入出力契約で疎結合にし、2つ目・3つ目を速く作れるようにする
- **既存を壊さず"読み足す"** — 稼働中のシステムは触らず、アダプタで新しいハブへ流し込む。移行は入口ごとのスイッチで段階的に

---

## 🌱 これから

これまでは一人で作ってきましたが、PR単位の開発・テスト・設計の文書化は自分で習慣にしてきました。次は、**現場に入るエンジニアとしてチームの中でレビューを受けながら**、業務システムと生成AI（OCR・文章生成・エージェント）の両方で専門性を深め、より大きな業務とデータに向き合いたいと考えています。

---

## 🔗 Links

- ✍️ Zenn：https://zenn.dev/takutoshuto
- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/
- 🐙 GitHub：https://github.com/takutoshuto-hash

<!--
差し替えメモ:
- OCR Trust Agent のリポジトリを公開したら、表の「結果発表まで非公開」を [コード](https://github.com/takutoshuto-hash/ocr-trust-agent) に差し替え（奨励賞の発表は 12/1）。
- Zenn の②「同時に使っても壊れない」③「WAF」を公開したら一覧の先頭に足し、ハイライト🔒の行に②のリンクを付ける。
- ピン留め（Customize your pins）は unified-order-model / social-post-agent / mail-triage-agent / gift-order-demo の順。
-->
