<!-- github.com/takutoshuto-hash のプロフィールREADME（takutoshuto-hash リポジトリの README.md）用ドラフト。
     公開後にZenn記事③のURLを差し替える箇所あり（下部コメント参照）。 -->

# 首藤卓登 (Takuto Shuto)

**業務理解 × 生成AI・クラウドで、現場の課題を「わかって・作って・運用する」内製エンジニア**

[![Zenn](https://img.shields.io/badge/Zenn-@takutoshuto-3EA8FF?logo=zenn&logoColor=white)](https://zenn.dev/takutoshuto)
[![Live Demo](https://img.shields.io/badge/Live_Demo-GiftDesk-2EA44F?logo=googlechrome&logoColor=white)](https://takutoshuto-hash.github.io/gift-order-demo/)

専門の開発部署がない食品・ホスピタリティ系の会社で、EC・Webマーケティングと社内システム開発を一人で兼任しています。現場の困りごとを、**要件定義 → 設計 → 実装 → 運用保守まで一人で**動くシステムにして解決してきました。外部委託・市販SaaSに頼らず、独学・ソロで内製するのが得意です。

扱う領域は **EC・受注・出荷・MEO・SEO・SNS・メール運用** と広く、技術も **Python / Google Apps Script / PHP / AWS / Google Cloud** と課題に合わせて選びます。生成AI（Claude / Gemini）は"道具の一つ"として、**OCR・文章生成・AIエージェント**など必要な形で業務に組み込みます。

---

## 🔑 実績ハイライト

- 🎁 **受注・出荷の業務システムを内製**（本命の"業務効率化"）— FAX手書き注文のOCR取り込みから、送り状CSV・出荷指示書・熨斗・請求まで1画面に統合。繁忙期は **月1,000〜2,000件** を処理
- 🗺️ **Googleマップ（GBP）運用を19施設ぶん内製化** — 業者見積で **年 約565万円相当を ¥0** 運用。滞留していた口コミ **約6,000件を3ヶ月で返信**し、返信率を実質100%へ
- 📈 **多店舗チェーンのSEOを半自動化** — ブログ経由の **検索クリックを約8.3倍** に（GA4 / Search Console × 生成AI）
- 📦 **EC出荷を別スタックで作り直し** — WordPress＋Welcart の自社ECで、入金確認（銀行CSV照合）〜発送完了メールを **PHP で1本のパイプライン**に
- 🤖 **AWSサーバーレス × Claude でAIエージェント** — 契約駆動 / Human-in-the-loop / 多層コストガードレールで、設計から約3週間で本番稼働

---

## 🛠 代表プロジェクト

| プロジェクト | 概要 | 主な技術 | リンク |
|---|---|---|---|
| **GiftDesk（受注管理）** | 申込入力から送り状CSV・指示書・熨斗・請求書までを1つのSPAに統合。FAX注文書はLLMで構造化抽出 | Google Apps Script / スプレッドシート / Gemini API | [ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **GBP/MEO 内製化** | 19施設の口コミ返信（AI下書き＋一括投稿）・数値監視・営業時間の改ざん検知・月次レポートを自作 | Python / Google Business Profile API / BigQuery / Looker Studio / Claude | *（記事は公開準備中）* |
| **多店舗SEO分析** | 制作会社任せだったGA4/GSCを自社に取り戻し、月次レポート＋ブログ運用を半自動化 | GA4 / Search Console / Python / BigQuery / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/850997ad982ff4) |
| **EC出荷支援（Welcart）** | 自社ECの入金確認〜発送メールを、Welcart管理画面を使わず専用アプリで一気通貫。DBに直結して業務に合う画面を"横に"自作 | PHP / MySQL / PDO / ヤマトB2 CSV | *（記事は公開準備中）* |
| **AX Marketing Hub** | Slackの自然文から Notion の事実を参照し、Instagram投稿案を月10件まとめて生成するAIエージェント | Python / AWS(Lambda・DynamoDB・EventBridge・SAM) / Claude / Notion / Slack | [解説記事](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)・[コード](https://github.com/takutoshuto-hash/social-post-agent) |
| **メール整理エージェント** | 受信メールを自動で仕分け・要約・ラベリングし、機械が下書き・人が確定する運用に | Python / AWS SAM / Claude | [コード](https://github.com/takutoshuto-hash/mail-triage-agent) |

---

## 📦 公開コード（GitHub）

- **[gift-order-demo](https://takutoshuto-hash.github.io/gift-order-demo/)** — 受注管理SPA（GiftDesk）の公開デモ
- **[social-post-agent](https://github.com/takutoshuto-hash/social-post-agent)** — SNS投稿案生成エージェント（Python / AWS SAM・サニタイズ版）
- **[mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent)** — メール整理エージェント（Python / AWS SAM・サニタイズ版）

---

## ✍️ 書いたもの（Zenn）

実務で作ったシステムの設計判断と落とし穴を記事にしています。→ **[zenn.dev/takutoshuto](https://zenn.dev/takutoshuto)**

- [Slackに一言で企業Instagramの投稿案が10件出る仕組みを、AWSサーバーレス×Claudeで作った](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)
- [制作会社任せだったアクセス解析を自社に取り戻し、月30分レポート＋週1本のSEOブログ運用にしたら検索クリックが8倍になった](https://zenn.dev/takutoshuto/articles/850997ad982ff4)

ほか、**GBP/MEO内製化・受注管理（GAS）・EC出荷（PHP）・手書き帳票のOCR** について順次公開しています。

---

## 🧰 技術スタック

- **言語**：Python / JavaScript（Google Apps Script）/ PHP / HTML・CSS
- **LLM・AI**：Anthropic API（Claude Sonnet・Haiku／Tool use・プロンプトキャッシュ）/ Gemini API / Google Cloud Vision API
- **クラウド・データ**：AWS（Lambda・DynamoDB・EventBridge・SAM）/ Google Cloud（Cloud Functions・Scheduler）/ BigQuery / Looker Studio / MySQL
- **連携・公開**：Slack API / Notion API / Google Business Profile API / GitHub Pages / Chrome拡張

---

## 💡 設計で大事にしていること

- **機械が下書き、人が承認（Human-in-the-loop）** — OCR・AI返信・入金/発送など、公開・課金・誤配送が絡む操作は必ず人が最終判断
- **制約が設計を強くする** — IT予算ゼロ・非IT人材が毎日使う、という制約を前提に「小さく作って価値を出す」
- **壊れにくく作る** — 列は名前で引く（位置を固定しない）・型を守る（先頭ゼロや長い伝票番号は文字列）・冪等制御で二重実行を防ぐ
- **取り消せない操作は3点セット** — 確認画面・ログ・取り消しを最初から入れる（メール送信・ステータス変更）
- **agents as tools（契約駆動）** — 生成AIを組む時は共通の入出力契約で疎結合にし、2つ目・3つ目を速く作れるようにする

---

## 🌱 これから

独学・ソロで積み上げてきた開発を、**チーム開発の中で正しい設計・技術を身につけながら**、より大きな課題に活かしたいと考えています。いま取り組んでいるのは、**チャネルごとにバラバラに作った受注・出荷システムを"1つの注文モデル"に統合**すること。あわせて、**生成AI（OCR・文章生成・エージェント）を実務・事業に落とし込む**領域にも力を入れています。

---

## 🔗 Links

- ✍️ Zenn：https://zenn.dev/takutoshuto
- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/
- 🐙 GitHub：https://github.com/takutoshuto-hash

<!--
公開後の差し替えメモ:
- 3本目（GBP/MEO）を公開したら、代表プロジェクト表の「（記事は公開準備中）」を
  [解説記事](https://zenn.dev/takutoshuto/articles/b589f1516c5052) に、
  「書いたもの（Zenn）」にも同記事を1行追加する。
- Welcart（PHP）記事を公開したら、同様に「（記事は公開準備中）」を実URLに差し替え。
-->
