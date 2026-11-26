# 首藤卓登 (Takuto Shuto)

**アナログだった会社に、業務システムと生成AIを自分で入れてきたエンジニア**

[![Zenn](https://img.shields.io/badge/Zenn-@takutoshuto-3EA8FF?logo=zenn&logoColor=white)](https://zenn.dev/takutoshuto)
[![Live Demo](https://img.shields.io/badge/Live_Demo-GiftDesk-2EA44F?logo=googlechrome&logoColor=white)](https://takutoshuto-hash.github.io/gift-order-demo/)
[![CI unified-order-model](https://github.com/takutoshuto-hash/unified-order-model/actions/workflows/ci.yml/badge.svg)](https://github.com/takutoshuto-hash/unified-order-model/actions)

IT の担当者がおらず、注文を **FAX と電話**で受けていた食品ギフトの会社で働いています。任された受注・出荷の不便を自分で解消しようと、GAS で仕組みを作り始めたのが出発点です。作り足すうちに増えたアプリは 2026年9月に **1つの自社アプリ**にまとめ、いまは出荷担当の3名が毎日使っています。

そこから担当が広がり、**Amazon の立ち上げ・自社EC・グループ19施設の Googleマップ・SEO と SNS** を受け持っています。どの担当も、生成AI（Claude / Gemini）と自作の仕組みで回しています。2026年11月には、販路ごとにばらばらだった数字を1つの画面に集めました。開発部署はなく、設計から実装、運用までを1人で持っています。

---

## 🗂 担当ごとにしていること

| 担当 | やっていること | AI・仕組み | 数字 |
|---|---|---|---|
| **受注・出荷** | 複数の入口の注文を1つの台帳で受け、出荷・請求まで | PHP + MySQL の自社アプリ。FAX・はがきは Gemini で読み取り | 5つのアプリを1つに。3名が毎日使う |
| **Amazon** | 販売担当として入社し、出品していなかったところから立ち上げ。広告の運用と分析、リサーチ | Amazon Ads API で数字を取り、毎週分析して見直す | 広告費の割合（TACOS）約61% → 約26〜34% |
| **自社EC** | リニューアル（デザイン・構築以外）、商品登録、企画、改修 | GA4・ヒートマップで分析し、自作の WordPress プラグインで直す | カートから購入に進む割合 約26% → 約37% |
| **Googleマップ（19施設）** | 口コミ返信と施設情報の管理 | Claude が返信案 → 自作のチェック → 人が OK → API で一括投稿 | たまっていた約6,000件を約3か月で。今は1日約5分 |
| **数字の見える化** | 販路ごとの数字を1か所に集める | 毎朝の API 取り込み（GA4・Search Console・Amazon Ads）と社内用の画面 | — |
| **SEO・SNS** | 自社サイト・自社EC・グループ店舗のサイトの検索対策、Instagram、LINE | 分析・企画・投稿づくりを定期タスクで自動化 | ブログ経由の検索クリック 132 → 1,093回 |

---

## 📦 公開しているコード

実務で動いているものを、会社の情報をダミーに置き換えて公開しています。外部 API につながなくてもテストが通ります。

| リポジトリ | 何か | 技術 | テスト / CI |
|---|---|---|---|
| **[unified-order-model](https://github.com/takutoshuto-hash/unified-order-model)** | 4つの受注システムでばらばらだった「注文」を1つのモデルにそろえる変換。本番 PHP の設計を TypeScript の型で表し直したもの | TypeScript（strict） / Vitest | Vitest 46ケース・GitHub Actions・[解説記事](https://zenn.dev/takutoshuto/articles/1485430c919762) |
| **[gift-order-demo](https://github.com/takutoshuto-hash/gift-order-demo)** | ギフトの受注管理アプリ「GiftDesk」の公開デモ。入力1回で送り状 CSV・指示書・熨斗・月次集計まで | HTML / CSS / Vanilla JS | [ライブデモ](https://takutoshuto-hash.github.io/gift-order-demo/) |

ほかに作ったもの: [social-post-agent](https://github.com/takutoshuto-hash/social-post-agent)（Slack の一言から Instagram の投稿案を作る AI エージェント）・[mail-triage-agent](https://github.com/takutoshuto-hash/mail-triage-agent)（受信メールを重要度で仕分けて Slack に知らせる AI エージェント）。どちらも Python / AWS SAM / Claude、pytest と GitHub Actions 付き。

---

## 🛠 担当ごとの中身

### 受注・出荷のシステム化
- FAX と電話で受け、作業ごとに別々の Excel で管理していた注文に、Web の申込と業務アプリを作った。カタログギフトに Web 申込を足し、**申込の約7割が Web** に
- 入口が増えるたびに作り足して5つになったアプリを、2026年9月に1つにまとめた
- 自社EC・Amazon・取引先の直送・カタログギフト（Web・はがき）・FAX・電話の注文を1つの台帳に取り込み、1件の注文から出荷日ごとに自動で作る:
  - ヤマト B2 の送り状データ（配達日数の表から出荷日を自動で決める）・伝票番号の取り込み
  - 出荷の指示書・送り状に貼るカード・熨斗（文字数で大きさを自動で決める）・工場への出荷依頼
  - 銀行の入金データとの照合、入金確認・発送・配達確認のメール
  - 請求書・月次の集計・販路ごとの売上
- 3名が同時に使っても壊れない作り（版番号の楽観ロック・採番の原子化・冪等な取り込み）
- 記事: [全体の流れ](https://zenn.dev/takutoshuto/articles/12562ee33ede1e)・[設計記録](https://zenn.dev/takutoshuto/articles/e12ef58cfe8f18)・[GiftDesk](https://zenn.dev/takutoshuto/articles/bc2ff859475742)・[手書き帳票の LLM×OCR](https://zenn.dev/takutoshuto/articles/a9e73fa4ed60ca)

### Amazon の立ち上げと運用
- 販売担当として入社し、出品者の登録から商品登録までを1人で行い、2025年10月に販売を開始
- 最初に売上を分析し、売れている商品と買っている人（個人・法人）の偏りを突き止めて、広告の配分を見直した
- 広告は実売上と突き合わせた数字で毎週分析して見直し、成果の出ない広告の停止や関係のない検索語の除外で **TACOS を約61%から約26〜34%に**。Amazon Ads API を申請から承認まで通し、取得・集計・予算の切り替えを自動化。金額の判断は人、キーワードの整理は AI という分担
- 競合の価格・画像・説明文と検索の言葉を調べて、出品ページを書き直した

### 自社EC のリニューアルと改善
- リニューアルでデザインと構築以外（制作会社の選定・撮影・要望の整理）を担当。足りない機能は自作プラグインで足した（購入手続きの案内・お届け日の計算・クーポン・請求書と領収書・GA4 の購入計測）
- GA4 とヒートマップでカゴ落ちを調べて購入手続きを改修。**カートから購入に進む割合が約26% → 約37%**
- 問い合わせの大半を占める営業メールを自動で振り分け。全社のセキュリティ点検も実施

### Googleマップ（グループ19施設）
- たまっていた口コミ **約6,000件を約3か月で返信**
- 毎朝の定期処理 → Claude が返信ルールに沿って返信案 → 自作のチェック（文字数・使わない言葉・直近の返信との重なり）→ 人が全文を読んで OK → API で一括投稿。人の作業は1日約5分
- 食の安全・法的な話など6種類の口コミは、返信案を作らず人に回す
- 検索の言葉のデータを施設ごとに分析し、API で施設の設定を直した
- 記事: [19施設の Googleマップ運用を内製した話](https://zenn.dev/takutoshuto/articles/b589f1516c5052)

### 販路ごとの数字の見える化
- 会社として数字を集めていなかったため、販路ごとの数字を棚卸しし、方針と台帳を決めてから社内用の画面を作った
- 毎朝の自動取り込み（GA4・Search Console・Amazon Ads API・Clarity・出荷と EC のデータベース）。数字を集める層は AI が無くても動き、判断と文章は AI が作る、の2層
- 分析用のデータベースには個人情報を入れない

### SEO と SNS
- 自社サイト・自社EC・グループ店舗のサイトで、Search Console と GA4 を毎月分析して書く記事と直すページを決め、分析と下書きを半自動に。グループ店舗のサイトでは**ブログ経由の検索クリック 132 → 1,093回**（2か月）、その後も前年同期の約3.5倍（[記事](https://zenn.dev/takutoshuto/articles/850997ad982ff4)）
- 自社EC では、AI 検索がサイトを読めない設定を見つけて直し、構造化データとよくある質問を整えた
- Instagram は数字の取得・企画・投稿づくりを毎週の定期タスクで回し、人は撮影と確認だけ。LINE は友だち限定クーポンと追加の経路を作った

---

## 🧪 個人開発・挑戦

- **Agentic AI Hackathon with Google Cloud（第5回）一次審査通過** — 手書きの FAX 注文書を Gemini で読み、根拠のある項目だけ自動で確定するエージェント。14日分のシミュレーションで、人が確かめる割合 **51% → 14%**（Python / Gemini / ADK / Cloud Run）。[概要記事](https://zenn.dev/takutoshuto/articles/0ba433ee0dbe33)
- **AtCoder Heuristic Contest 074（With AI 部門）** — 初参加で **532人中237位**。Claude Code を自動で起動し、解答を採点して良ければ採用する改善ループを自作
- **AI エージェントの安全装置** — AI が秘密のファイルを読んだり危ない操作をしたりしないよう止める仕組みを、自分の作業環境に入れた。ダミーの秘密で破れるかを試し、破られた手口も記録
- **WordPress のプラグイン** — 日本のネットショップ向け（ふりがな・郵便番号から住所・のし・お届け日の指定）。WordPress.org の審査を通って公開
- **家庭用の LINE ボットとアレクサ** — お酒の価格比較とレシピの提案（GAS / Claude API）

---

## 🧰 技術スタック

- **言語**：Python / PHP / JavaScript・TypeScript（GAS・React）/ SQL
- **生成AI**：Claude API（モデルの使い分け・構造化出力・プロンプトキャッシュ）/ Gemini API（画像の読み取り）/ Google ADK / Claude Code
- **クラウド・データ**：AWS（Lambda・DynamoDB・EventBridge・SAM）/ Google Cloud（Cloud Run・Cloud Functions・BigQuery・Looker Studio）/ MySQL
- **つないだサービス**：Amazon Ads API / Google Business Profile API / GA4・Search Console / ヤマトB2クラウド / WordPress・Welcart / Slack・Notion API
- **開発の作法**：Git・GitHub（PR 単位）/ pytest・Vitest / GitHub Actions

---

## 💡 設計で大事にしていること

- **AI が下書き、人が確かめてから外に出す** — 口コミ返信・FAX の読み取り・広告の金額など、取り消せないものは人が最後に判断する
- **使う人の作業から作る** — 自分が任された不便から作り始め、使われ方を見て直す
- **増えたら、まとめ直す** — 稼働中のシステムは止めず、入口ごとに切り替えて1つにした
- **数字は元データから確かめる** — 台帳ではなく元の CSV から計算し直し、API の数字は管理画面と突き合わせてから使う

---

## 🌱 これから

これまでは1人で作ってきました。PR 単位の開発・テスト・設計の文書化は自分で習慣にしてきましたが、書いたコードを見てくれる人がいません。次は**現場に入るエンジニアとして、レビューのあるチームで**、業務システムと生成AIの仕事をしたいと考えています。

---

## 🔗 Links

- ✍️ Zenn：https://zenn.dev/takutoshuto
- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/

<!--
差し替えメモ:
- ハッカソンのリポジトリを公開したら、個人開発の行にコードのリンクを足す（奨励賞の発表は 12/1）。
- ピン留め（Customize your pins）は unified-order-model / gift-order-demo / social-post-agent / mail-triage-agent の順。
-->
