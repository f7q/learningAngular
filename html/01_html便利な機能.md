# gridスタイル

divタグに追加するのにdisplay:gridが有効

```html

<div [style]="'display: grid; grid-template-columns: 100px 100px 50px; grid-template-columns: 20px 20px; gap: 0px;'">
  <div>A</div>
  <div>B</div>
  <div>C</div>
  <div>A2</div>
  <div>B2</div>
  <div>C2</div>

</div>

```

こういったグリッドが表現できる。業務用のUIを表現したい時は、stretchでラベルを張り付けたりして反映できるので便利

| A | B | C |  
|---|---|---|  
| A2 | B2 | C2 |

※ `stretch` とは2025年にChromeブラウザ標準で使えるようになった機能で、heightやwidthで100%指定だと見切れてしまったりフィットしてくれないが、この機能を使うことで、表示領域内に綺麗に収まるように再計算して反映できます。
