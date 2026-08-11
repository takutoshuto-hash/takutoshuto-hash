# 首藤卓登 (Takuto Shuto)

食品ギフト企業（社名は非公開）で、EC・Webマーケティングと並行して、**社内の業務システムを内製開発**しています。専門の開発部署がない環境で、現場の困りごとを **自分で動くシステムにして解決する** ことを続けてきました。独学で Google Apps Script や Python、LLM API を使い、外部委託・市販SaaSに頼らず内製化するのが得意です。最近は **AWS サーバーレス上で動く AIエージェント** の開発にも取り組んでいます。

- 🛠 要件定義 → 設計 → 実装 → 運用保守までを一人で担当（ソロ開発）
- 🤖 Gemini・Claude（Anthropic）API を実務で活用（OCR／文章生成／AIエージェント）
- 💡 「誰がどう使うか」から逆算し、小さく作って価値を出すスタイル

---

## 開発した主なシステム

### 🤖 AX Marketing Hub｜投稿案生成AIエージェント（AWSサーバーレス）

Slackの自然文メッセージから、Notionの情報を参照して **Instagram投稿案を自動生成・保存するAIエージェント**。生成は Claude Sonnet 5、意図抽出・分類は Haiku 4.5 と用途でモデルを使い分け、**Tool use（function calling）ループ** で1回の呼び出しから10件の投稿案を構造化生成します。将来的に Amazon・GBP 運用も同じ基盤に載せ、**AIがAIを束ねる多エージェント構成（AX化）** へ拡張する設計で、本エージェント（IG AI）はその第一弾です。

- **技術：** Python／Anthropic API（Claude Sonnet 5・Haiku 4.5／Tool use・プロンプトキャッシュ）／AWS（Lambda・DynamoDB・EventBridge・SAM）／Slack API／Notion API
- **設計：** 契約駆動設計（agents as tools）／Human-in-the-loop（公開・課金は必ず人が承認）／冪等制御（SHA256）・サーキットブレーカー・スペンドリミットの多層コストガードレール
- **状態：** Slack起動 → Notion参照 → 投稿案の生成・保存までを実機で一気通貫で確認済み（運用実績はこれから蓄積）。記載の数値は実装仕様上の値です。

### 🎁 GiftDesk｜ギフト受注管理システム

申込入力から請求書まで **15機能をブラウザ上のSPAに統合**。1回の入力で、送り状CSV・出荷指示書・熨斗・月次集計・請求書へ自動連携します。FAX注文書は **Gemini API（マルチモーダルLLM）で項目を構造化抽出（JSON）**。

- **技術：** Google Apps Script／スプレッドシート／Gemini API／HTML・CSS・JavaScript（SPA）
- **規模：** 繁忙期は月 1,000〜2,000 件の受注を処理。担当者はスプレッドシートに直接触れない設計。
- 🔗 **ライブデモ（ダミーデータ）：** https://takutoshuto-hash.github.io/gift-order-demo/

### 📍 GBP自社運用システム｜17施設のGoogleビジネスプロフィール運用

グループ17施設の口コミ返信（AI生成＋一括投稿）、検索順位の観測、月次レポート生成を内製化。**API → BigQuery → Looker Studio の監視基盤** を構築し、レポート文面は **Claude API** で自動生成しています。

- **技術：** Google Apps Script／BigQuery／Looker Studio／Claude API／Chrome拡張
- **成果：** 外部委託なら年間約400〜700万円相当の運用を内製で ¥0 化。口コミ返信率100%を維持し、来店行動指標を施策前比 **+66.7%（実測）** に改善。

### 📦 カタログギフト受注管理システム

QR/Web申込受付・ハガキのOCR読み取り・出荷CSV・指示書自動生成・Amazon注文取込を、**一気通貫でデータ化**。

- **技術：** GitHub Pages／Google Apps Script（8ファイル構成）／OCR
- **成果：** 月 50〜100件の申込を1人で処理。入力ミス率を約5%→0.5%未満に低減。

### 🚚 直送ギフト申込システム（2ブランド）

24時間対応のWeb申込、**銀行CSVによる入金の自動マッチング**、出荷指示書の自動生成、追跡番号の一括メール通知。FAX・手作業中心だった直送業務をWeb・自動化に置き換えました。

- **技術：** Google Apps Script／スプレッドシート／Webフォーム
- **展開：** 同一アーキテクチャを複数ブランドへ横展開。

> ※ 各システムは外部委託・市販SaaSに頼らず内製。GAS製システムの運用は原則 Google 無料枠内（¥0）で、顧客データを扱うOCRのみ、学習利用を避けるため有料枠を選択しています。AX Marketing Hub は AWS・LLM の従量課金上で動きますが、スペンドリミット等のコストガードレールで小さく抑えています。数値は自社の実測・見積りに基づく範囲で記載しています。

---

## 技術スタック

- **言語：** JavaScript（Google Apps Script）／Python／HTML／CSS
- **LLM・AI：** Anthropic API（Claude Sonnet 5・Haiku 4.5／Tool use・プロンプトキャッシュ）／Gemini API／Google Cloud Vision API（過去）
- **クラウド・データ：** AWS（Lambda・DynamoDB・EventBridge・SAM）／Google スプレッドシート／BigQuery／Looker Studio
- **連携・公開：** Slack API／Notion API／GitHub Pages／Chrome拡張
- **設計：** agents as tools（契約駆動設計）／Human-in-the-loop／冪等制御・サーキットブレーカー・コストガードレール

---

## これから

独学・ソロで積み上げてきた開発を、**チーム開発の中で正しい設計・技術を身につけながら、より大きな課題に活かしたい**と考えています。特に LLM を実務・事業に落とし込む領域に関心があり、現在は「agents as tools」でエージェントを設計し、**AIがAIを束ねる多エージェント基盤（AX化）** へと発展させる取り組みを進めています。

## リンク

- 🔗 ライブデモ（GiftDesk）：https://takutoshuto-hash.github.io/gift-order-demo/
- 🐙 GitHub：https://github.com/takutoshuto-hash

- 
