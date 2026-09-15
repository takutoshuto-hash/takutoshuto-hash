# 首藤卓登 (Takuto Shuto)

**業務理解 × 生成AI・クラウドで、現場の課題を「わかって・作って・運用する」内製エンジニア**

[![Zenn](https://img.shields.io/badge/Zenn-@takutoshuto-3EA8FF?logo=zenn&logoColor=white)](https://zenn.dev/takutoshuto)
[![Live Demo](https://img.shields.io/badge/Live_Demo-GiftDesk-2EA44F?logo=googlechrome&logoColor=white)](https://takutoshuto-hash.github.io/gift-order-demo/)

専門の開発部署がない食品・ホスピタリティ系の会社で、EC・Webマーケティングと社内システム開発を一人で兼任しています。現場の困りごとを、**要件定義 → 設計 → 実装 → 運用保守まで一人で**動くシステムにして解決してきました。外部委託・市販SaaSに頼らず、独学・ソロで内製するのが得意です。最近は **AWS サーバーレス上で動く AIエージェント** の開発に注力しています。

---

## 🔑 実績ハイライト

- 🤖 **AWSサーバーレス × Claude でAIエージェントを設計・運用** — *agents as tools*（契約駆動）／Human-in-the-loop／多層コストガードレールで、設計から約3週間で本番稼働
- 🗺️ **Googleマップ（GBP）運用を19施設ぶん内製化** — 業者見積で **年 約565万円相当を ¥0** 運用。滞留していた口コミ **約6,000件を3ヶ月で返信**し、返信率を実質100%へ
- 📈 **多店舗チェーンのSEO運用を半自動化** — ブログ経由の **検索クリックを約8.3倍** に（月次レポート＋ブログ生成をGA4/GSC×生成AIで）
- 🎁 **受注管理SPA（GAS）を内製** — 1回の入力で送り状CSV・指示書・熨斗・請求まで自動連携。繁忙期は **月1,000〜2,000件** を処理

---

## 🛠 代表プロジェクト

| プロジェクト | 概要 | 主な技術 | リンク |
|---|---|---|---|
| **AX Marketing Hub** | Slackの自然文から Notion の事実を参照し、Instagram投稿案を月10件まとめて生成するAIエージェント | Python / AWS(Lambda・DynamoDB・EventBridge・SAM) / Claude / Notion / Slack | [解説記事](https://zenn.dev/takutoshuto/articles/86c04c2a747f17) |
| **GBP/MEO 内製化** | 19施設の口コミ返信（AI下書き＋一括投稿）・数値監視・営業時間の改ざん検知・月次レポートを自作 | Python / Google Business Profile API / BigQuery / Looker Studio / Claude | *（記事は公開準備中）* |
| **多店舗SEO分析** | 制作会社任せだったGA4/GSCを自社に取り戻し、月次レポート＋ブログ運用を半自動化 | GA4 / Search Console / Python / BigQuery / Claude | [解説記事](https://zenn.dev/takutoshuto/articles/850997ad982ff4) |
| **GiftDesk（受注管理）** | 申込入力から送り状CSV・指示書・熨斗・請求書までを1つのSPAに統合。FAX注文書はLLMで構造化抽出 | Google Apps Script / スプレッドシート / Gemini API | [ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |
| **直送 / カタログギフト受注** | Web・ハガキOCR・Amazon取込・銀行CSVの入金消込・追跡番号通知を内製で一気通貫 | GAS / GitHub Pages / OCR(Vision/Gemini) | — |
| **メール整理エージェント**（公開コード） | 毎朝の受信メールをAIが重要度★1〜5で仕分けし、🔴🟠だけをSlackに要約通知。返信下書きも生成（自動送信はしない） | Python / AWS SAM / Claude / Gemini / IMAP | [コード](https://github.com/takutoshuto-hash/mail-triage-agent) |
| **AX Marketing Hub** | Slackの自然文から Notion の事実を参照し、Instagram投稿案を月10件まとめて生成するAIエージェント | Python / AWS(Lambda・DynamoDB・EventBridge・SAM) / Claude / Notion / Slack | [解説記事](https://zenn.dev/takutoshuto/articles/86c04c2a747f17) ・ [コード](https://github.com/takutoshuto-hash/social-post-agent) |

---

## ✍️ 書いたもの（Zenn）

実務で作ったシステムの設計判断と落とし穴を記事にしています。→ **[zenn.dev/takutoshuto](https://zenn.dev/takutoshuto)**

- [Slackに一言で企業Instagramの投稿案が10件出る仕組みを、AWSサーバーレス×Claudeで作った](https://zenn.dev/takutoshuto/articles/86c04c2a747f17)
- [制作会社任せだったアクセス解析を自社に取り戻し、月30分レポート＋週1本のSEOブログ運用にしたら検索クリックが8倍になった](https://zenn.dev/takutoshuto/articles/850997ad982ff4)

---

## 🧰 技術スタック

- **言語**：Python / JavaScript（Google Apps Script）/ HTML・CSS / PHP
- **LLM・AI**：Anthropic API（Claude Sonnet・Haiku／Tool use・プロンプトキャッシュ）/ Gemini API / Google Cloud Vision API
- **クラウド・データ**：AWS（Lambda・DynamoDB・EventBridge・SAM）/ Google Cloud（Cloud Functions・Scheduler）/ BigQuery / Looker Studio / MySQL
- **連携・公開**：Slack API / Notion API / Google Business Profile API / GitHub Pages / Chrome拡張

---

## 💡 設計で大事にしていること

- **agents as tools（契約駆動）** — エージェントは共通の入出力契約で疎結合にし、2つ目・3つ目を速く作れるようにする
- **機械が下書き、人が承認（Human-in-the-loop）** — 公開・課金が動く操作は必ず人が最終判断
- **多層のコストガードレール** — 冪等制御・サーキットブレーカー・スペンドリミットで、ひとり運用でも暴走させない
- **制約が設計を強くする** — IT予算ゼロ・非IT人材が毎日使う、という制約を前提に「小さく作って価値を出す」

---

## 🌱 これから

独学・ソロで積み上げてきた開発を、**チーム開発の中で正しい設計・技術を身につけながら**、より大きな課題に活かしたいと考えています。特に **LLMを実務・事業に落とし込む領域**に関心があり、「agents as tools」で複数エージェントを束ねる基盤（AX化）へと発展させる取り組みを進めています。

---

## 🔗 Links

- ✍️ Zenn：https://zenn.dev/takutoshuto
- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/
- 💻 公開コード（メール整理エージェント）：https://github.com/takutoshuto-hash/mail-triage-agent
- 💻 公開コード（投稿案生成エージェント）：https://github.com/takutoshuto-hash/social-post-agent
- 🐙 GitHub：https://github.com/takutoshuto-hash
