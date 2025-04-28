# 4. ルーティング（Routing）

## 主要な構成要素
- ルーティングモジュール（RouterModule）  
  Angular では、RouterModule.forRoot(routes) や RouterModule.forChild(routes) を使用して、アプリケーション内のすべてのルートを定義します。
- ルート定義（Routes）  
  各ルートは、パス（URL の一部）と、それに対応するコンポーネント、さらにはルートガードなどのオプション設定を持っています。
- ルーティングアウトレット（`<router-outlet>`）  
  テンプレートに `<router-outlet>` を配置し、ルーティングされたコンポーネントを動的にレンダリングする場所を指定します。
- ルートガード  
  認証やアクセス制御のため、特定のルートにアクセスできるかどうかを判断する仕組み（例: CanActivate、CanDeactivate）。

## 基本的な設定方法
以下は、シンプルなルーティング設定の例です。

a. ルート定義ファイルの作成
```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', component: HomeComponent },           // デフォルトルート
  { path: 'about', component: AboutComponent },       // /about で AboutComponent を表示
  { path: '**', redirectTo: '' }                      // 存在しないパスはホームへリダイレクト
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```
b. ルーティングアウトレットの配置
```html
<!-- app.component.html -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```
c. プログラムでのナビゲーション
```typescript
// 例: コンポーネント内でルーターのナビゲーションを実行
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-navigation',
  template: `<button (click)="goToAbout()">About へ移動</button>`
})
export class NavigationComponent {
  constructor(private router: Router) {}

  goToAbout(): void {
    this.router.navigate(['/about']);
  }
}
```
