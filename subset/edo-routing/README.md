# edo-routing 用サブセット

`maps.chizutodesign.com/edo-routing` の地図ラベルで実際に使う文字だけを残した
LINE Seed JP のグリフPBF。**このディレクトリは edo-routing 専用**で、
親ディレクトリの `LINESeedJP-Regular` / `LINESeedJP-Bold`（全文字）は
他の作品が使っているのでそのまま残してある。

## なぜ要るか

edo-routing の地図ラベルに出る文字は **479種**しかないのに、全範囲のPBFを
配信していたため、初期表示だけで **2.53MB / 38ファイル**を取っていた。
サブセット後は **244KB**（約10分の1）。

漢字はUnicode上に散らばっているので、479文字でも76の範囲にまたがる。
つまり**ファイル本数は減らず、1本あたりが軽くなる**（MapLibreは256文字ごとの
範囲単位でしか取りに行けないため）。

## 作り方

フォント本体は使わない。**親ディレクトリの既存PBFから、使わないglyphを
落としているだけ**なので、SDFの焼き方が変わらず見た目は1ピクセルも変わらない。

生成スクリプトは edo-routing 側にある:
`chizutodesign/edo-routing` の `tools/subset-glyphs.mjs`

使う文字は `index.html` のノードデータ（`mapLabel`）から機械的に列挙している。
**宿場や都市を追加したら焼き直しが要る。** 忘れると、その文字だけ豆腐（□）になる。
