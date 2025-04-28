# TypeScript
他の言語と比較して特殊な仕様は以下の通り。
1. 静的型付けと型注釈
2. 型推論
3. インターフェースと型エイリアス
4. ユニオン型、交差型、タプル型、リテラル型
5. ジェネリクス
6. 列挙型 (Enums)
7. アクセス修飾子 (public, private, protected)
8. デコレーター (Experimental)
9. 高度な型システム（条件型、マッピング型、ユーティリティ型）
10. 宣言ファイル (.d.ts)

## 1. 静的型付けと型注釈
- JavaScript は動的型付け言語ですが、TypeScript では変数や関数、クラスなどに明示的な型注釈を付与でき、コンパイル時に型の整合性をチェックします。
- メリット: 型エラーを事前に検出できるため、大規模なコードベースや複雑なアルゴリズムの信頼性・保守性が向上します。
- 例： 
```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

let age: number = 30;
```

## 2. 型推論
- 概要: 型注釈を明示しなくても、TypeScript のコンパイラは変数の初期値などから型を自動的に推論します。
- メリット: 開発者は冗長な型記述を避けつつ、型安全性を享受できるため、コードの可読性と生産性が向上します。
- 例:
```typescript
let message = "Hello, world!"; // message は string と推論される
```

## 3. インターフェースと型エイリアス
- インターフェース (Interface):
  - 目的: オブジェクトの構造やクラスの契約を定義するために使います。
  - 例:
```typescript
interface Person {
  name: string;
  age: number;
}

function printPerson(p: Person) {
  console.log(`${p.name} is ${p.age} years old.`);
}
```

- 型エイリアス (Type Alias):
  - 目的: 型に別名を与えて、複雑な型やユニオン型・交差型をわかりやすく記述します。
  - 例:
```typescript
type ID = number | string;
```

## 4. ユニオン型、交差型、タプル型、リテラル型

- ユニオン型 (Union Type):
  - 概要: 変数が複数の型のどれかであることを表現します。
  - 例:
```typescript
function format(input: string | number): string {
  return input.toString();
}
```

- 交差型 (Intersection Type):
  - 概要: 複数の型を組み合わせ、全ての型の性質を持つ型を表現します。
  - 例:
```typescript
type A = { a: number };
type B = { b: string };
type AB = A & B; // { a: number, b: string }
```

- タプル型 (Tuple Type):
  - 概要: 固定の要素数と各要素の型を明確にした配列を定義できます。
  - 例:
```typescript
let point: [number, number] = [10, 20];
```

- リテラル型 (Literal Type):
  - 概要: 具体的な値そのものを型として扱い、文字列や数値の特定の値のみを許容します。
  - 例:
```typescript
type Direction = "up" | "down" | "left" | "right";
```

## 5. ジェネリクス
- 概要: 型パラメータを利用することで、関数やクラス、インターフェースを様々な型に対して再利用可能にします。
- メリット: 型安全性を維持しつつ、柔軟で再利用可能なコードの作成が可能です。
- 例:
```typescript
function identity<T>(arg: T): T {
  return arg;
}

// 使用例
let output = identity<string>("TypeScript");
```

## 6. 列挙型 (Enums)
- 概要: 数値や文字列の定数を名前付きの集合体として定義でき、コードの可読性と保守性を高めます。
- 例:
```typescript
enum Color {
  Red,
  Green,
  Blue
}

let c: Color = Color.Green;
```

## 7. アクセス修飾子 (public, private, protected)
- 概要: クラスのプロパティやメソッドに対して、アクセスレベルを明示できます。これにより、内部実装のカプセル化とクラス設計が行いやすくなります。
- 例:
```typescript
class Employee {
  public name: string;
  private salary: number;
  protected department: string;
  
  constructor(name: string, salary: number, department: string) {
    this.name = name;
    this.salary = salary;
    this.department = department;
  }
}
```

## 8. デコレーター (Experimental)
- 概要: クラス、メソッド、プロパティ、アクセサ、パラメータに対してメタデータや振る舞いを追加する仕組みです。Angular など、多くのフレームワークで利用されています。
- 注意: 実験的な機能として用いられており、tsconfig.json で "experimentalDecorators": true を有効にする必要があります。
- 例:クラスデコレータ
```typescript
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class MyClass {
  // クラス実装
}
```

## 9. 高度な型システム（条件型、マッピング型、ユーティリティ型）
- 概要: TypeScript は最新バージョンで、条件型、マッピング型、そして組み込みのユーティリティ型（例えば、Partial<T>, Readonly<T>, Pick<T, K> など）を利用できます。これらにより、既存の型を変形したり新しい型を計算的に作り出すことが可能になります
- 例 (マッピング型):
```typescript
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

## 10. 宣言ファイル (.d.ts)
- 概要: JavaScript のライブラリや既存のコードに対して、型情報を付与するために宣言ファイルを利用できます。これにより、JavaScript 由来のコードも TypeScript の型安全性で取り扱うことができます。

 
