<div align="center">

# 地震情報可視化ツール      eqs viewer
**v 1.1.1b**
**ブラウザ完結型の地震・津波情報ダッシュボード**

 [[https://skotm.github.io/eqs-viewer/](https://skotm.github.io/eqs-viewer/)]

</div>

## プロジェクト概要

`eqs viewer` は地図上に地震情報や津波情報を描画するWebアプリケーションです。
、気象庁の公式データベースから取得した過去の地震記録（CSV）をドラッグ＆ドロップで可視化する機能を備えています。

## 詳細機能 (Features)

### 1. 高精度な地理情報マッピングと分析
- **過去の地震の震度表示**: 観測点の震度と、地域の最大震度の表示を切り替え可能。
 <img width="1824" height="1074" alt="image" src="https://github.com/user-attachments/assets/8c201116-eb88-484c-975d-cfc03464f37b" />

- **津波予報区のハイライト表示**: 気象庁のGISデータを基にした正確な海岸線描写により、津波警報・注意報の発表エリアを可視化。
  <img width="1665" height="992" alt="image" src="https://github.com/user-attachments/assets/5ab56bbe-118f-43a4-a3b9-af3d8150cc3b" />

- **推計震度分布のオーバーレイ**: 地震発生後の推計震度分布（500mメッシュ相当）を地図上に重畳表示。(設定で表示可)
  <img width="1663" height="995" alt="image" src="https://github.com/user-attachments/assets/bb2c9e45-f01f-4c1e-95ce-859b214a61ec" />

- **過去地震検索機能**:気象庁のデータベースから、各種条件を指定して過去の地震を検索し、地図上に情報を表示。(非公式)


### 2. 過去データのインポート機能 (CSV)
- **気象庁 震度データベース対応**: [気象庁 震度データベース検索](https://www.data.jma.go.jp/svd/eqdb/data/shindo/index.html) からダウンロードした過去の地震CSVファイルをそのまま読み込み可能。
- 地図上への即時プロットにより、過去の巨大地震の震度分布や震源などを視覚的に振り返ることができます。

### 3. モダンなUI/UX
- **完全ブラウザ動作**: バックエンドサーバー不要。HTML/JS/CSSのみで動作。
- **レスポンシブ & ダークモード**: PC、タブレット、スマートフォンに対応。リキッドグラスをイメージしたデザイン。

##  ディレクトリ構成 (Directory Structure)

     eqs-viewer
     ┣  index.html                  # メインのアプリケーションUI・ロジック
     ┣  japan.geo.json              # 日本地図のベースポリゴンデータ
     ┣  japan_centroids.json        # 各地域の中心座標データ
     ┣  震央地名.geo.json           # 気象庁が定義する震央地域のポリゴン
     ┣  津波予報区.json             # 津波予報区画の海岸線データ
     ┣  stations_with_amp_revised.json # 地震観測点データ
     ┗  README.md

## 使い方とセットアップ (Usage)

本ツールはフロントエンドのみで完結しているため、環境構築は非常に簡単です。

### オンラインで即座に利用する
以下のリンクから、ブラウザ上ですぐに利用可能です。
👉 [[https://skotm.github.io/eqs-viewer/](https://skotm.github.io/eqs-viewer/)]

## データソースと引用元 (Data Sources & Credits)

本プロジェクトは、以下の公開データおよびライブラリを利用・加工して作成されています。データの開発者様に深く感謝申し上げます。

### 地図・地理データ
- **気象庁 防災情報XML GISデータ**
  - URL: [https://www.data.jma.go.jp/developer/gis.html](https://www.data.jma.go.jp/developer/gis.html)
  - 用途: `japan.geo.json`（日本地図ベース）および `津波予報区.json`（海岸線データ）の作成元データ。
- **JMA_Region (0Quake様)**
  - URL: [https://github.com/0Quake/JMA_Region](https://github.com/0Quake/JMA_Region)
  - 用途: `震央地名.geo.json` として、気象庁の震央地名をポリゴン描画するために利用。

### 地震・観測点データ
- **全国の地震観測点座標リスト (iku55様 Gist)**
  - URL: [https://gist.github.com/iku55/79005d1896631ad6117bbe327b8162c1](https://gist.github.com/iku55/79005d1896631ad6117bbe327b8162c1)
- **J-SHIS 地震ハザードステーション (防災科学技術研究所)**
  - URL: [https://www.j-shis.bosai.go.jp/labs/wm2020/](https://www.j-shis.bosai.go.jp/labs/wm2020/)
  - 用途: 上記iku55様のリストをベースに、J-SHISのデータを参照して観測点の地盤増幅特性を加工し、`stations_with_amp_revised.json` として利用。
- **気象庁 震度データベース**
  - URL: [https://www.data.jma.go.jp/svd/eqdb/data/shindo/index.html](https://www.data.jma.go.jp/svd/eqdb/data/shindo/index.html)
  - 用途: 本ツールのCSV読み込み機能の対象フォーマット。
             過去地震検索の情報ソース。
### 使用ライブラリ
- **Leaflet (v1.9.4)**: [https://leafletjs.com/](https://leafletjs.com/) - 地図レンダリング
- **Turf.js (v6.5.0)**: [https://turfjs.org/](https://turfjs.org/) - 空間・ポリゴン演算

## 免責事項 (Disclaimer)

> [!WARNING]
> - 本ツールは個人開発のプロジェクトであり、提供される情報の正確性、速報性、完全性を保証するものではありません。
> - アプリケーションの遅延やバグにより、実際の情報と異なる表示がされる可能性があります。
> - **実際の避難行動や生命の安全に関わる判断には、必ず[気象庁の公式発表](https://www.jma.go.jp/)や各自治体の指示を確認してください。**
> - 本ツールの利用により生じた直接的・間接的ないかなる損害についても、開発者（skotm）は一切の責任を負いません。

## ライセンス (License)

このプロジェクトは [MIT License](LICENSE) の下で公開されています。詳細については `LICENSE` ファイルをご覧ください。

---
<div align="center">
Developed by <b><a href="https://github.com/skotm">skotm</a></b>
</div>
