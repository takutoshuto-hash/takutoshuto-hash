# 首藤卓登 (Takuto Shuto)

**業務理解 × 生成AI・クラウドで、現場の課題を「わかって・作って・運用する」内製エンジニア**

[![Zenn](https://img.shields.io/badge/Zenn-@takutoshuto-3EA8FF?logo=zenn&logoColor=white)](https://zenn.dev/takutoshuto)
[![Live Demo](https://img.shields.io/badge/Live_Demo-GiftDesk-2EA44F?logo=googlechrome&logoColor=white)](https://takutoshuto-hash.github.io/gift-order-demo/)
[![CI mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/mail-triage-agent/actions)
[![CI social-post-agent](https://github.com/takutoshuto-hash/social-post-agent/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/social-post-agent/actions)
[![CI unified-order-model](https://github.com/takutoshuto-hash/unified-order-model/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/unified-order-model/actions)

専門の開発部署がない食品・ホスピタリティ系の会社で、EC・Webマーケティングと社内システム開発を一人で兼任しています。現場の困りごとを、**要件定義 → 設計 → 実装 → 運用保守まで一人で**動くシステムにして解決してきました。直近では、チャネルごとにバラバラだった4つの受注・出荷システムを「1つの注文モデル」に統合し、PHP + MySQL の自社アプリとして**本番移行まで完了**させています。

扱う領域は **EC・受注・出荷・MEO・SEO・SNS・メール運用** と広く、技術も **Python / Google Apps Script / PHP / AWS / Google Cloud** と課題に合わせて選びます。生成AI（Claude / Gemini）は"道具の一つ"として、**OCR・文章生成・AIエージェント**など必要な形で業務に組み込みます。

---

## 📦 まず見てほしい公開コード

実務で動いているものを、固有情報をダミーに置き換えて公開しています。**テストと CI 付き**で、外部APIに接続せずに `pytest` / `vitest` が通ります。

| リポジトリ | 何か | 技術 | テスト / CI |
|---|---|---|---|
| **[unified-order-model](https://github.com/takutoshuto-hash/unified-order-model)** | 4つの受注システムでバラバラだった「注文」を1つのモデルにそろえる変換。依頼主がいない注文・空のお届け先・旧システムのステータスを型で止める（本番 PHP の設計を TypeScript で表し直したもの） | TypeScript（strict） / Vitest | Vitest 46ケース（型のテストを含む）・GitHub Actions（Node 20〜24）・[解説記事](https://zenn.dev/takutoshuto/articles/1485430c919762) |
| **[social-post-agent](https://github.com/takutoshuto-hash/social-post-agent)** | Slackの一言から Notion の事実を参照して Instagram 投稿案を月10件生成するAIエージェント（本番稼働中のものの公開版） | Python / AWS Lambda・DynamoDB・EventBridge・SAM / Claude / Gemini | pytest 41ケース・GitHub Actions |
| **[mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent)** | 毎朝の受信メールを重要度で仕分けし、重要なものだけ Slack に届けるAIエージェント。返信は下書きまで（人が送る） | Python / AWS SAM / Claude / Gemini / IMAP | pytest 57ケース・GitHub Actions（3.11〜3.13） |
| **[gift-order-demo](https://github.com/takutoshuto-hash/gift-order-demo)** | 受注管理SPA「GiftDesk」の公開デモ。入力1回で送り状CSV・指示書・熨斗・月次集計まで | HTML / CSS / Vanilla JS（単一ファイル） | [ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **OCR Trust Agent** | 手書きFAX注文書を Gemini で読み、根拠のある項目だけ自動確定し、人の修正から学んで要確認を減らすエージェント（Agentic AI Hackathon with Google Cloud vol.5 応募作） | Python / Gemini / ADK / Cloud Run / Cloud Scheduler | pytest 240ケース超。審査期間中は非公開（面接時に画面共有できます）・[概要記事](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33) |

2つのエージェントは共通の「契約駆動（agents as tools）」基盤の上に作っていて、Human-in-the-loop・冪等・コストガードレールの考え方をそろえています。

---

## 🔑 実績ハイライト

- 📦 **4つの受注・出荷システムを"1つの注文モデル"に統合し、PHP + MySQL の自社アプリとして本番移行**（稼働中）— 入金確認（銀行CSV照合）〜送り状CSV〜出荷指示書〜追跡番号取込〜発送完了メールを1画面のパイプラインに。旧システムは壊さず"読み足す"アダプタで接続（[設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)）
- 🎁 **受注・出荷の業務システムを内製** — FAX手書き注文のOCR取り込みから、送り状CSV・出荷指示書・熨斗・請求まで1画面に統合。繁忙期は **月1,000〜2,000件** を処理
- 🗺️ **Googleマップ（GBP）運用を19施設ぶん内製化** — 業者見積で **年 約565万円相当を ¥0** 運用。滞留していた口コミ **約6,000件を3ヶ月で返信**し、返信率を実質100%へ
- 📈 **多店舗チェーンのSEOを半自動化** — ブログ経由の **検索クリックを約8.3倍** に（GA4 / Search Console × 生成AI）
- 🤖 **AWSサーバーレス × Claude でAIエージェント** — 契約駆動 / Human-in-the-loop / 多層コストガードレールで、設計から約3週間で本番稼働

---

## 🛠 代表プロジェクト

| プロジェクト | 概要 | 主な技術 | リンク |
|---|---|---|---|
| **受注・出荷の統合（統一注文モデル）** | 自社EC・直送ギフト・カタログギフト・Amazon・はがき/FAXの注文を1つのモデルに正規化し、出荷業務を1画面化。本番移行済み | PHP / MySQL / PDO / ヤマトB2 CSV | [設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)・[PHP出荷支援の記事](https://zenn.dev/takutoshuto/articles/ae8ed60e00a0ca)・[型で表し直したコード](https://github.com/takutoshuto-hash/unified-order-model) |
| **GiftDesk（受注管理）** | 申込入力から送り状CSV・指示書・熨斗・請求書までを1つのSPAに統合。FAX注文書はLLMで構造化抽出 | Google Apps Script / スプレッドシート / Gemini API | [解説記事](https://zenn.dev/takutoshuto/articles/bc2ff859475742)・[ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **手書き帳票のLLM×OCR** | 自作OCRで挫折し、Cloud Vision → Gemini にたどり着くまで。ハッカソンでは「信頼が育つ」エージェントへ発展 | Gemini API / Cloud Vision / Python | [解説記事](https://zenn.dev/takutoshuto/articles/a9e73fa4ed60ca)・[エージェント版](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33) |
| **GBP/MEO 内製化** | 19施設の口コミ返信（AI下書き＋一括投稿）・数値監視・営業時間の改ざん検知・月次レポートを自作 | Python / Google Business Profile API / BigQuery / Looker Studio / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/b589f1516c5052) |
| **多店舗SEO分析** | 制作会社任せだったGA4/GSCを自社に取り戻し、月次レポート＋ブログ運用を半自動化 | GA4 / Search Console / Python / BigQuery / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/850997ad982ff4) |
| **AX Marketing Hub** | Slackの自然文から Notion の事実を参照し、Instagram投稿案を月10件まとめて生成するAIエージェント | Python / AWS(Lambda・DynamoDB・EventBridge・SAM) / Claude / Notion / Slack | [解説記事](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)・[コード](https://github.com/takutoshuto-hash/social-post-agent) |
| **メール整理エージェント** | 受信メールを自動で仕分け・要約・ラベリングし、機械が下書き・人が確定する運用に | Python / AWS SAM / Claude | [コード](https://github.com/takutoshuto-hash/mail-triage-agent) |

---

## ✍️ 書いたもの（Zenn・9本）

実務で作ったシステムの設計判断と落とし穴を記事にしています。→ **[zenn.dev/takutoshuto](https://zenn.dev/takutoshuto)**

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

- **言語**：Python / JavaScript（Google Apps Script）/ PHP / SQL / HTML・CSS
- **LLM・AI**：Anthropic API（Claude／Tool use・プロンプトキャッシュ・構造化出力）/ Gemini API（マルチモーダル）/ Google ADK / Google Cloud Vision API
- **クラウド・データ**：AWS（Lambda・DynamoDB・EventBridge・SAM・S3）/ Google Cloud（Cloud Run・Cloud Functions・Scheduler・Cloud Storage）/ BigQuery / Looker Studio / MySQL
- **開発の作法**：pytest（外部APIはモック）/ GitHub Actions / IaC（AWS SAM・Dockerfile）/ Git
- **連携・公開**：Slack API / Notion API / Google Business Profile API / GitHub Pages / Chrome拡張

---

## 💡 設計で大事にしていること

- **機械が下書き、人が承認（Human-in-the-loop）** — OCR・AI返信・入金/発送など、公開・課金・誤配送が絡む操作は必ず人が最終判断
- **制約が設計を強くする** — IT予算ゼロ・非IT人材が毎日使う、という制約を前提に「小さく作って価値を出す」
- **壊れにくく作る** — 列は名前で引く（位置を固定しない）・型を守る（先頭ゼロや長い伝票番号は文字列）・冪等制御で二重実行を防ぐ
- **取り消せない操作は3点セット** — 確認画面・ログ・取り消しを最初から入れる（メール送信・ステータス変更）
- **agents as tools（契約駆動）** — 生成AIを組む時は共通の入出力契約で疎結合にし、2つ目・3つ目を速く作れるようにする
- **既存を壊さず"読み足す"** — 稼働中のシステムは触らず、アダプタで新しいハブへ流し込む

---

## 🌱 これから

独学・ソロで積み上げてきた開発を、**チーム開発の中で正しい設計・技術を身につけながら**、より大きな課題に活かしたいと考えています。統合した注文モデルの上に、**生成AI（OCR・文章生成・エージェント）を実務・事業に落とし込む**領域へ力を入れています。

---

## 🔗 Links

- ✍️ Zenn：https://zenn.dev/takutoshuto
- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/
- 🐙 GitHub：https://github.com/takutoshuto-hash

<!--
差し替えメモ:
- OCR Trust Agent のリポジトリを公開したら、表の「審査期間中は非公開」を [コード](https://github.com/takutoshuto-hash/ocr-trust-agent) に差し替え。
- ピン留め（Customize your pins）は social-post-agent / mail-triage-agent / gift-order-demo の順。
-->
