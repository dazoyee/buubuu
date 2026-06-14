# CLAUDE.md

このリポジトリで作業する AI エージェント（Claude Code）向けの指針です。
人間の貢献者向けの詳細な手順・規約は [CONTRIBUTING.md](./CONTRIBUTING.md) を、概要は [README.md](./README.md) を参照してください。

## プロジェクト概要

「ぶーぶーランド」は2歳児向けの「はたらくのりもの」知育PWA。
`index.html` 1ファイルにアプリ本体・全コンテンツ・SVG・音声合成を内包し、`manifest.webmanifest` と `service-worker.js` を加えた**静的3ファイル**で完結する。GitHub Pages（`dazoyee/buubuu`）で公開している。

## 絶対制約（変更してはいけない前提）

- **完全オフライン**: 実行時に外部API・バックエンド・CDNを一切呼ばない。すべて同梱データで完結させる。
- **ビルド不要**: バンドラ・トランスパイラを導入しない。そのまま静的ホスティングに置ける形を保つ。
- **フレームワーク不使用**: 素の HTML/CSS/JS のみ。React 等を入れない。
- **単一HTML構成**: アプリのロジック・スタイル・データは `index.html` に内包する。
- **相対パス**: アセット参照・`start_url`・SW登録はすべて相対パス（`./`）。サブパス配信（`/buubuu/`）で動くこと。
- **コンテンツのトーン**: 2歳児向け＝やさしい・短い・前向き・ひらがな中心。怖い／事故の描写を入れない。

## 主要データの場所（`index.html` 内）

- `VEHICLES`: のりもの18種（名前・オノマトペ・効果音タイプ・やさしい一言 ほか）
- `VEHICLE_ART` / `vehicleBody()` / `buildVehicleSVG()`: のりもののアニメ付きSVGイラスト生成
- `STORIES`: 名前差し込み式のお話32話（`{name}` プレースホルダ、`short`／`long`）
- `SOUND_PARAMS` / `playSound()`: Web Audio による効果音合成
- `APP_VERSION`: スタート画面に表示するバージョン

## AI 特有の作業ガイド

- **描画の確認**: UI/SVG を変更したら、ヘッドレス Chrome でスクリーンショットを撮り、ランタイムエラーが無いことと見た目を確認する。
- **構文チェック**: `index.html` の `<script>` を抽出して `node --check`、`service-worker.js` も `node --check`。
- **データ整合**: のりもの・お話・効果音の参照（`id`／`shape`／`sound`）が一致しているか検証する。
- **リリース時のバージョン更新**: `index.html` の `APP_VERSION` と `service-worker.js` の `CACHE` を必ず一緒に更新する（詳細は CONTRIBUTING.md の「バージョニング」を参照）。
- **コーディング規約・コミット規約**: [CONTRIBUTING.md](./CONTRIBUTING.md) に従う。
