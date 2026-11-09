# スキルガイド — 高度Web・デザイン担当

Claude Code で Web・デザイン業務に使えるスキルの紹介と使い分けです。
スキルは `/スキル名` で明示的に呼び出せるほか、依頼内容に合えば Claude が自動で使います。

> 注意：ここに挙げたスキルの多くは、この環境に導入済みのプラグイン（`frontend-design`, `design`, `design-skills`, `superpowers` など）由来です。
> 別の環境では入っていないことがあるので、使えない場合は `/plugin` で同名プラグインを導入してください。
> リポジトリ固有のスキル（`/optimize-prompt`, `/prompt-retro`）は `.claude/skills/` にあり、clone すれば常に使えます。

---

## 1. まず押さえる中核スキル（優先度：高）

| スキル | 何をするか | 使う場面 |
|---|---|---|
| `frontend-design:frontend-design` | テンプレ感のない、意図のあるUI・ビジュアル方向性の決定と実装 | LP、サイト、Webアプリ画面を新規に作る／作り直す |
| `design-skills:design-elevation` | 機能的な出力を「作り込まれた」デザインへ引き上げる（Tailwindトークン基準） | HTML、ダッシュボード、資料など見た目の仕上げ全般 |
| `design-skills:design-critique` | ユーザビリティ原則・UXの法則に基づく構造化レビュー | 自分の成果物のセルフレビュー、既存サイトの診断 |
| `design-skills:accessibility-audit` | WCAG 2.2（A/AA/AAA）監査と修正コード提示 | 公開前チェック、改修時 |
| `design-skills:design-systems` | トークン・コンポーネント・命名の設計と監査 | 複数ページ／複数人で運用するサイト |

## 2. フェーズ別スキル一覧

### 戦略・リサーチ
- `design-skills:ux-strategy` — 事業目標とUXをつなぐ戦略、優先順位付け
- `design-skills:journey-mapping` — カスタマージャーニー／サービスブループリント
- `design:user-research` / `design-skills:ux-research` — インタビュー設計、ユーザビリティテスト計画
- `design:research-synthesis` — 調査結果の統合、インサイト抽出

### 情報設計・UX
- `design-skills:interaction-design` — 画面遷移、状態設計、マイクロインタラクション
- `design-skills:ux-writing` / `design:ux-copy` — CTA、エラーメッセージ、空状態などのマイクロコピー

### ビジュアル・実装
- `frontend-design:frontend-design` — アートディレクションと実装（上記）
- `anthropic-skills:ui-ux-pro-max` — UIスタイル・配色・フォントペアリングの幅広いリファレンス
- `dataviz` — チャート、KPIタイル、ダッシュボードの配色とレイアウト
- `adobe-for-creativity:adobe-fonts` — Adobe Fonts の検索・組み合わせ提案
- `adobe-for-creativity:adobe-design-from-template` / `adobe-create-social-variations` — バナー、SNS画像などの固定サイズ制作物
- `artifact-design` — 共有用のHTMLページ（Artifact）を作るときの設計ルール

### 品質保証
- `design:accessibility-review` — WCAG 2.1 AA の簡易監査
- `design:design-critique` / `design-superpowers:design-review` — 階層・一貫性のレビュー
- `code-review` — 実装コードのバグ検出
- `run` — アプリを起動して実際の表示・動作を確認
- `superpowers:verification-before-completion` — 完了宣言前の検証手順

### 体系化・引き渡し
- `design-skills:design-systems` / `design:design-system` — デザインシステムの監査・拡張・ドキュメント化
- `design:design-handoff` — レイアウト・トークン・状態・ブレークポイントを含む開発向け仕様書
- `design-skills:design-ops` — デザインスプリント、レビュー体制、QAプロセス

### 進め方（プロセス系）
- `superpowers:brainstorming` — 作る前に要件と方向性を詰める
- `superpowers:writing-plans` → `superpowers:executing-plans` — 大きめの実装を計画して実行
- `superpowers:systematic-debugging` — 表示崩れや不具合の原因調査

### プロンプト・ナレッジの改善
- `/optimize-prompt`（本リポジトリ） — ざっくりした依頼をデザインブリーフに変換、または既存プロンプトの改善
- `/prompt-retro`（本リポジトリ） — 作業の振り返りから CLAUDE.md・テンプレートの改善案を作る
- `anthropic-skills:skill-creator` / `superpowers:writing-skills` — 定型業務を新しいスキルとして切り出す
- `platform-skills:self-improve` — 学びの記録と、繰り返し出るパターンのルール化

## 3. 典型的な組み合わせ例

**新規LPを作る**
`/optimize-prompt` → `superpowers:brainstorming` → `frontend-design:frontend-design` → `run`（スクショ確認） → `design-skills:design-critique` → `design-skills:accessibility-audit` → `/prompt-retro`

**既存サイトのリニューアル診断**
`design-skills:design-critique` + `design-skills:accessibility-audit` → `design-skills:ux-strategy`（改善の優先度付け） → `design:design-handoff`

**デザインシステム構築**
`design-skills:design-systems`（監査） → トークン定義 → コンポーネント実装 → `design:design-system`（ドキュメント化）

## 4. 追加を検討してよいもの

- **Figma 連携**（`plugin:design:figma` MCP）：デザインデータの読み込み・ハンドオフに有効。現在のクラウド環境ではネットワーク制限で接続できていないため、使う場合は環境の許可ホスト設定が必要。
- **Playwright**：環境にプリインストール済み。スクリーンショット比較やビジュアル回帰テストに使える。
- **Lighthouse / axe-core**：パフォーマンス・a11y の自動計測をCIに組み込む場合に導入を検討。
