# Wizarding World of Inversion

高校2年生向け「倒置」の語順並べ替えゲーム。単語が書かれた石をドラッグ（またはタップ）して並べ、
正しい語順で「呪文を唱える」と石が宝石に変わります。全7問。

- 公開URL（GitHub Pages 有効化後）: https://champagne-neko.github.io/English-grammar-apps/
- 配布用QRコード: [`qr.png`](qr.png)（上のURLが入っています）

## 構成

| 項目 | 採用したもの | 理由 |
| --- | --- | --- |
| アプリ本体 | `index.html` 1ファイル（HTML / CSS / 素のJavaScript） | ビルド不要・ライブラリ不要。先生が問題文を直接書き換えられる |
| ドラッグ操作 | Pointer Events | マウス・指・ペンを同じコードで扱える。iPad / Chromebook / スマホで動く |
| 効果音 | Web Audio API で合成 | 音声ファイル不要。右上で ON/OFF |
| 読み上げ | Web Speech API（`speechSynthesis`） | 正解後に「英文を聞く」で音読モデルを再生 |
| ホスティング | GitHub Pages | 無料・広告なし・ログイン不要。生徒はURLを開くだけ |
| 配布 | QRコード（`qr.png`） | 授業スライドやプリントに貼って読み取らせる |

生徒の回答データはどこにも送信しません（個人情報を扱わない）。

## 収録問題（倒置 7問）

易しい順に並べ、「文頭の語 → 助動詞が主語の前へ跳ぶ」動きを繰り返し体験できるようにしています。
各問に1つ、典型的な誤りを表す **偽りの石**（ダミー）を混ぜています。

| # | 例文 | 型 | 偽りの石 |
| --- | --- | --- | --- |
| 1 | 500 Neither have I. | Neither＋助動詞＋S | did |
| 2 | 494 Never did I dream of making a fortune … | 否定の副詞＋did＋S＋原形 | dreamed |
| 3 | 495 Little did we think that he would lose the game. | Little＋did＋S＋think | thought |
| 4 | 498 Only recently have I realized … | Only＋副詞＋have＋S＋p.p. | did |
| 5 | 496 At no time have I been more nervous than I am now. | 否定の副詞句＋have＋S | I have |
| 6 | 497 Not only do the workers want a pay increase, but … | Not only＋do＋S＋V | does |
| 7 | 508 Among the audience were the President and her daughter. | 場所の句＋V＋S | was |

502（so did the airlines）は「the airlines did so」も正しい英文になり、答えが一つに決まらないので外しました。
503 以降（so / such の語順、省略、強調構文）は倒置とは別の型なので、今回は入れていません。

## 問題の追加・変更

`index.html` の `PROBLEMS` 配列を編集します。1問はこの形です。

```js
{
  no: 494, spell: "Never ― 夢見ずの呪文", gem: "Ruby", color: "#e0455a",
  jp: "株式市場に投資して財産を築くなどとは、夢にも思わなかった。",
  prefix: "",                                   // 石の前に固定表示する部分
  suffix: "by investing in the stock market.",  // 石の後に固定表示する部分
  tiles: [["Never", "neg"], ["did", "aux", true], ["I", "S"], ["dream", "V"], ["of making a fortune", "O"]],
  decoys: ["dreamed"],                          // 偽りの石
  pattern: [["否定の副詞", true], ["助動詞", true], ["主語"], ["動詞の原形"], ["…"]],  // ヒントの巻物
  normal: "I never dreamed of making a fortune by investing in the stock market.",
  inverted: "<em>Never did I dream</em> of making a fortune by investing in the stock market.",
  tip: "否定語が文頭に来たら、疑問文と同じ語順になる。…"
}
```

`tiles` の並びがそのまま正解です。3つ目の `true` は宝石になったときに光らせる石（主語の前へ跳ぶ語）。
強調構文（514 It was not until … that ～ など）も同じ形で追加できます。

## デプロイ手順（GitHub Pages）

1. この作業ブランチを `main` にマージする。
2. GitHub のリポジトリ画面 → **Settings → Pages**。
3. **Build and deployment → Source** を「Deploy from a branch」、Branch を `main` / `/ (root)` にして Save。
4. 1〜2分後に https://champagne-neko.github.io/English-grammar-apps/ で開けるようになる。
5. `qr.png` をスライドやプリントに貼る。

無料プランの GitHub Pages は **公開リポジトリ** でのみ使えます。リポジトリを非公開にしたい場合は、
`index.html` を [Netlify Drop](https://app.netlify.com/drop) にドラッグするだけでも公開できます（その場合はURLが変わるので、QRコードを作り直してください）。

## 授業での使い方の例

- 1問ごとに「ふつうの語順 → 倒置の呪文」の比較が出るので、正解後に全員で英文を音読する。
- 「英文を聞く」で読み上げを流し、手で石を動かした語順と音を結びつける。
- 最後の「宝物庫」画面（一発成功の数と称号）をスクリーンショットで提出させると、取り組み状況が分かる。

## 動作確認

`index.html` をブラウザで直接開けば、そのまま遊べます（サーバー不要）。
