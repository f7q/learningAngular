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

# QA
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
