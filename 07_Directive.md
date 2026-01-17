# 5. ディレクティブ（Directive）
この機能はWPFだとbehaviorに近い、カスタムディレクティブでツールチップを作ったり、子ダイアログをクリック＆ドロップで移動させたりに使用できる。

- *ngIf 条件が真の場合にだけ、対象の要素を DOM にレンダリングします。
- *ngFor 配列やコレクションの各要素に対してテンプレートを繰り返し生成します。
- [ngSwitch] スイッチの対象となる値をバインドします。
  - *ngSwitchCase 条件に一致する場合に表示されるテンプレートを定義します。
  - *ngSwitchDefault いずれの条件にもマッチしなかった場合のデフォルトテンプレートです。
- [ngClass] 条件に応じて CSS クラスを動的に付加または除去します。
- [ngStyle] インラインスタイルを動的に適用します。
- [(ngModel)] フォーム要素に対して双方向データバインディングを実現するディレクティブです。（※ FormsModule をインポートする必要があります。）
- ngNonBindable このディレクティブが適用された部分は、Angular のバインディング処理を無効にし、通常のテキストとして表示させるときに使用します。
- ngTemplateOutlet 指定したテンプレートを動的にレンダリングするためのディレクティブです。
- ngComponentOutlet 動的にコンポーネントを生成し、レンダリングするためのディレクティブです。（高度な利用ケースで使用されます。）

```html
<!-- ngIf -->
<div *ngIf="isVisible">この内容は isVisible が true のときに表示されます</div>
<!-- ngFor -->
<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
<!-- ngSwitch -->
<div [ngSwitch]="value">
  <p *ngSwitchCase="'A'">値はAです</p>
  <p *ngSwitchCase="'B'">値はBです</p>
  <p *ngSwitchDefault>どちらでもありません</p>
</div>
<!-- ngClass -->
<div [ngClass]="{'active': isActive, 'disabled': !isActive}">
  クラスが動的に適用されます
</div>
<!-- ngStyle -->
<div [ngStyle]="{'background-color': bgColor, 'font-size': fontSize + 'px'}">
  スタイルが動的に設定されます
</div>
<!-- ngModel -->
<input [(ngModel)]="userName" placeholder="名前を入力してください">
<!-- ngNonBindable -->
<div ngNonBindable>
  ここでは {{ expression }} などの Angular バインディングは適用されません。
</div>
<!-- ngTemplateOutlet -->
<ng-container *ngTemplateOutlet="templateRef; context: myContext"></ng-container>
```
