# 3. サービス（Service）

例：
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

// サービスクラスは、アプリケーション全体で利用できる共通機能を提供します。
// @Injectable デコレーターにより、依存性注入（DI）の対象としてクラスを定義します。
// providedIn: 'root' とすることで、アプリ全体でシングルトンとして扱われます。
@Injectable({
  providedIn: 'root'
})
export class DataService {
  // API エンドポイントの URL（必要に応じて変更してください）
  private apiUrl = 'https://api.example.com/data';

  // HttpClient をコンストラクタで DI（依存性注入）することで後で利用できます。
  constructor(private http: HttpClient) {}

  // API からデータを取得するメソッドの例
  // Observable<any> 型で返すため、非同期通信の結果を購読（subscribe）して扱えます。
  getData(): Observable<any> {
    return this.http.get<any>(this.apiUrl);
  }

  // API に新しいデータを追加するメソッドの例
  addData(newData: any): Observable<any> {
    return this.http.post<any>(this.apiUrl, newData);
  }
}
```
## 説明
- @Injectable デコレーター このデコレーターを使用することで、Angular の DI コンテナにこのクラスを登録し、どこからでも注入できるようになります。providedIn: 'root' と指定すれば、アプリ全体でシングルトンインスタンスとして利用可能です！
- HttpClient の利用 HTTP 通信を行うために、HttpClient をコンストラクタに注入しています。これにより、外部 API との GET や POST リクエストなどを簡単に実装できます。
- Observable を返す メソッドは Observable を返しており、呼び出し元で subscribe することで、非同期処理の結果を受け取れます。

## 注入の宣言箇所
@NgModule／@Componentデコレーターのprividersパラメーターに引き渡す。
```typescript
export abstract class IService {
  abstract getData(): string;
}

export class RealService implements IService {
  getData() { return 'Real data'; }
}

// アプリケーション設定を定義したオブジェクト
const APP_CONFIG = {
  apiUrl: 'https://api.example.com',
  timeout: 5000
};
export class LoggerService {
  log(message: string) { console.log(message); }
}
export class ApiService {
  constructor(private baseUrl: string) {}
  getData() { return `Data from ${this.baseUrl}`; }
}

// ファクトリ関数を定義
export function apiServiceFactory(config: { apiUrl: string }): ApiService {
  // ここで何らかのロジックを適用
  return new ApiService(config.apiUrl);
}
// プロバイダー設定で useClass を利用して依存性を登録
providers: [
  { provide: RealService, useClass: RealService }, // これは省略可能（デフォルトの挙動）
  { provide: IService, useClass: RealService }, // DI のトークンとして IService を使い、実装を RealService に差し替え
  { provide: 'AppConfig', useValue: APP_CONFIG }, // プロバイダー設定で useValue を使用
  LoggerService,
  { provide: 'AppLogger', useExisting: LoggerService }, // LoggerService を e.g. 'AppLogger' トークンのエイリアスとしても利用する
  {
    provide: ApiService,
    useFactory: apiServiceFactory, // プロバイダー設定で useFactory を使用
    deps: ['AppConfig']  // ファクトリ関数で必要な依存性を注入
  }
]
```
- useClass: 単純にクラスからインスタンスを生成する場合に利用、インスタンスはimplicitです。（インターフェース実装の差し替えや、実装の交換にも便利）。
- useValue: 定数・設定情報・既に生成されたオブジェクトを DI で提供したい場合に適用。
- useExisting: 2 つ以上のトークンで同じインスタンスを共有する必要があるとき（エイリアスとして使う）。
- useFactory: ファクトリ関数で動的にインスタンス化や値生成が必要な場合に利用（単にインスタンス生成ではなく処理を挟みたい場合）。

