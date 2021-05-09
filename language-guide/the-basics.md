# The Basics

最終更新日: 2020/5/9

Swift は iOS, macOS, watchOS, tyOS のアプリ開発のための新しいプログラミング言語です。一方で、 Swift の多くの部分は C 言語と Objective-C の開発経験から馴染みのある感じを受けるでしょう。

Swift は C 言語と Objective-C の全ての基本的な型に対応した Swift バージョンの型を提供します。 integer に対する `Int`、floating-point に対する `Double` と `Float`、Boolean に対する `Bool`、text データに対する `String`があります。また、3 つのより強力な collection 型(`Array`, `Set`, `Dictionary` )も提供します。詳細は [Collection Types](./language-guide/../collection-types.md)に記載。

C 言語のように、Swift は名前を特定することで、値を保持したり、その値を参照するために変数を使います。また、Swift は変数の値を変更できなくすることで、より幅広い方法で変数を利用しています。これらは定数として知られており、C 言語の定数よりもかなり強力です。定数は、値を変更する必要がない場合に、定数を利用することで、コードを意図的に、より安全に、よりわかりやすくするために Swift 全体で利用されます。

馴染みのある型に加え、Swift は Objective-C にはなかった、tuple のようなより応用的な型を導入します。tuple は値を 1 つのグループとして扱うことができます。tuple を使うと、関数から複数の値を 1 つの値の組み合わせとして返すことができます。

Swift は値が存在しないかもしれない値を扱う optional 型を導入します。optional は、「値が存在していて、これは x と等しい」もしくは「値は一切存在しない」ということを伝えます。optional は Objective-C のポインタと `nil` を扱うのに似ていますが、class だけではなく、あらゆる型に利用することができます。Objective-C の `nil` ポインタよりも、安全で表現的なだけでなく、多くの Swift の最も強力な特徴のコアな部分になります。

Swift は型安全な言語です。つまり、言語がコードで扱う値の型を明確にしてくれます。`String` が必要な場合、この型安全な特徴が、間違って `Int` を渡してしまうことを防いでくれます。同様に、型安全なことで、optional ではない `String` に optional の `String` を気がつかずに渡してしまうことも防いでくれます。型安全なことで、開発プロセスの中でできる限り早くエラーに気がついて、修正する手助けをしてくれます。

## Constants and Variables

定数と変数は特定の型の値(`10`、`"Hello"`など)と名前(`maximumNumberOfLoginAttempts`、`welcomeMessage`など)を関連付けます。定数は一度値を設定すると変更することはできません。一方で変数は先々に異なった値を設定できます。

### Declaring Constants and Variables

定数と変数は、使用する前に定義されていなければなりません。定数は `let`、変数は `var` キーワードで定義します。ここにユーザが何回ログインをしようとしたか(試行回数)を追跡する定数と変数の例を紹介します。

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

このコードは下記のように読み取れます。

「`maximumNumberOfLoginAttempts`と呼ばれる定数を定義して、`10`という値を設定します。次に`currentLoginAttempt`という変数を定義して、`0`という初期値を設定する」

この例では、最大回数は変更しないので、定数で定義しています。試行回数はログインを試みる度に増加させなければならないため、変数として今の試行回数を定義しています。

1 行の中で、カンマで区切って複数の定数や変数を定義することもできます。

```swift
var x = 0.0, y = 0.0, z = 0.0
```

> NOTE  
> コードで保持している値がこの先変更されない場合は、 `let` を使って定数として定義しましょう。
> 変数は変更できるようにする必要がある場合にのみ使用しましょう。

### Type Annotations

定数や変数を定義する時に、保持する値の種類をより明確にするために、型アノテーションを使用することもできます。定数や変数の名前の後にコロンを置いて、型アノテーションを書きましょう。

この例では `welcomeMessage` という変数に型アノテーションを書いて `String` が保持されることを示しています。

```swift
var welcomeMessage: String
```

定義の中のコロンは、「~型の~」を意味します。なので、このコードは下記のように読み取れます。

「`String`型の`welcomeMessage`という変数を定義する」

「`String`型の」というフェーズは、どんな`String`型の値も保持できることを意味します。つまり、保持することができる「物の型(物の種類)」だと考えましょう。

`welcomeMessage`にはエラーなしに文字列を設定できます。

```swift
welcomeMessage = "Hello"
```

1 行の中で、同じ型の複数の変数をカンマで区切って定義することもできます。この際、型アノテーションは最後の変数の後に 1 つ付けます。

```swift
var red, green, blue: Double
```

> NOTE  
> 実際に型アノテーションを書く必要はあまりありません。定義時に定数や変数に初期値を与えた場合、
> Swift はたいていそれらの型を推論できます(詳細は[Type Safety and Type Inference](#type-safety-and-type-inference))。
> 上記の`welcomeMessage`の例では、初期値を与えていないため、推論をすることができないため、`welcomeMessage`変数は型アノテーションで型を特定しています。

### Naming Constants and Variables

定数名と変数名には、Unicode 文字も含めた、ほとんどの文字を含めることができます。

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

定数名と変数名に、ホワイトスペース、数学記号、矢印、公式ではない Unicode スカラ値、罫線素片罫線素片、書式文字は含められません。また、数字から始めることはできません(他の位置に数字を含めることはできます)

一度特定の型で定数や変数を定義すると、同じ名前で再定義することはできません。また、異なる型の値を保持することもできません。定数を変数に、変数を定数に変換することもできません。

> NOTE  
> Swift の予約語と同じ名前で定数や変数を使いたい場合、そのキーワードをバッククォート(``)で囲みます。
> とはいうものの、予約語を名前に使用することは、本当に他に選択肢がない以外は避けましょう。

既存の変数の値を他の互換性のある型の値に変更することができます。この例では、`friendlyWelcome`の値を`"Hello!"`から`"Bonjour!"`に変更しています。

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

変数とは異なり、定数の値は最初に設定した後に変更できません。試みようとしても、コンパイル時にエラーになります。

```swift
let languageName = "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.
```

### Printing Constants and Variables

`print(_:separator:terminator:)`関数を使って、定数や変数の現在の値を出力することができます。

```swift
print(friendlyWelcome)
// Prints "Bonjour!"
```

`print(_:separator:terminator:)`関数はグローバル関数で、1 つ以上の値を適切なアウトプット先に出力します。Xcode では、`print(_:separator:terminator:)`関数を使うと、
Xcode のコンソールパネルへ値を出力します。`separator` と `terminator`引数には、デフォルト値が用意されているので省略可能です。デフォルトでは、最後に改行を追加します。改行を付けたくない場合は、`terminator`に空文字を渡しましょう。例えば`print(someValue, terminator: "")`。詳細は[Default Parameter Values](./functions.md#default-parameter-values)。

Swift はより長い文字列の中で定数や変数をプレースホルダとして使用したい場合、 string interpolation\(文字列補間\)を使い、定数や変数の現在値に置き換えるように Swift に伝えることができます。名前を括弧(())で囲み、開始括弧の前にバックスラッシュ(\\)を付けます。

```swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!"
```

> NOTE  
> string interpolation\(文字列補間\)で使用できるオブションは[String Interpolation](./strings-and-characters.md#string-interpolation)に記載しています
## Comments

## Semicolons

## Integers

### Integer Bounds

### Int

### UInt

## Floating-Point Numbers

## Type Safety and Type Inference

## Numeric Literals

## Numeric Type Conversion

### Integer Conversion

### Integer and Floating-Point Conversion

## Type Aliases

## Booleans

## Tuples

## Optionals

### nil

### If Statements and Forced Unwrapping

### Optional Binding

### Implicitly Unwrapped Optionals

## Error Handling

## Assertions and Preconditions

### Debugging with Assertions

### Enforcing Preconditions

