# その他

vscode 
- 差分機能あり
- LiveServer機能（プラグイン）
- Angular Language Service → Angularのコード補完やエラーチェックを強化
- Angular Snippets → よく使うコードを簡単に入力できるスニペット集
- Prettier – Code formatter → コードの整形を自動化し、統一感を持たせる
- NX Console → Angularのモノレポ管理に便利なツール
- angular2-switcher → `.html` ⇄ `.ts` の切り替えをショートカットで実行
- Path Intellisense → ファイルパス補完を強化し、入力ミスを防ぐ
- ESLint → TypeScriptのコード品質を向上させる静的解析ツール
- Debugger for Chrome → TypeScriptのデバッグを簡単に行える拡張機能
- Jest → TypeScriptのテスト環境を強化するユニットテスト用プラグイン
- TypeScript Hero → 型情報の補完やインポートの管理を簡単にする
- Pretty TypeScript Errors → TypeScriptのエラーメッセージを見やすく整形

# QA1
angular 画面追加したけど表示されません、何かコマンド実施すれば解決する？

1. ビルドのキャッシュをクリア
```sh
ng build --clean
# または
rm -rf node_modules package-lock.json && npm install
```
2. 開発サーバーを再起動
```sh
ng serve --force
# または
npm start
```
3. ルーティングの問題をチェック
```sh
ng generate module app-routing --flat --module=app
```
4. 変更検知を強制実行
```sh
ng build --watch
```

# QA2
ViewChildで#をつかった書き方があるのですが、あれは何ですか？  
  
# を使った書き方は テンプレート参照変数 を定義するためのものです。 Angular のテンプレート内で #変数名 のように記述すると、その要素を参照するための変数を作成できます。  
  
例えば、以下のようなコードがあります。
```html
<input #myInput type="text">
<button (click)="logValue()">ログ</button>
```
この #myInput は テンプレート参照変数 であり、コンポーネントの TypeScript 側で @ViewChild を使って取得できます
```typescript
import { Component, ViewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  @ViewChild('myInput') myInput!: ElementRef;

  logValue() {
    console.log(this.myInput.nativeElement.value);
  }
}
```

# QA3
テンプレート参照変数があると別の要素に渡せます。
```html
<app-child>
  <input #myInput type="text" (input)="myValue = myInput.value"/>
  <input type="text" [value]="myValue"/>
</app-child>
```
