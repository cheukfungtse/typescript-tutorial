# 陣列的类型

在 TypeScript 中，陣列类型有多种定义方式，比较灵活。

## 「类型 + 方括号」表示法

最简单的方法是使用「类型 + 方括号」来表示陣列：

```ts
let fibonacci: number[] = [1, 1, 2, 3, 5];
```

陣列的项中**不允许**出现其他的类型：

```ts
let fibonacci: number[] = [1, '1', 2, 3, 5];

// index.ts(1,5): error TS2322: Type '(number | string)[]' is not assignable to type 'number[]'.
//   Type 'number | string' is not assignable to type 'number'.
//     Type 'string' is not assignable to type 'number'.
```

上例中，`[1, '1', 2, 3, 5]` 的类型被推断为 `(number | string)[]`，这是联合类型和陣列的结合。

陣列的一些方法（method）的参数也会根据数组在定义时约定的类型进行限制：

```ts
let fibonacci: number[] = [1, 1, 2, 3, 5];
fibonacci.push('8');

// index.ts(2,16): error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.
```

上例中，`push` 方法只允许传入 `number` 类型的参数，但是却传了一个 `string` 类型的参数，所以报错了。

## 陣列泛型

也可以使用陣列泛型（Array Generic） `Array<elemType>` 来表示数组：

```ts
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

关于泛型，可以参考[泛型](../advanced/generics.md)一章。

## 用接口表示陣列

接口(interface)也可以用来描述陣列：

```ts
interface NumberArray {
    [index: number]: number;
}
let fibonacci: NumberArray = [1, 1, 2, 3, 5];
```

`NumberArray` 表示：只要 `index` 的类型是 `number`，那么值的类型必须是 `number`。

## any 在陣列中的应用

一个比较常见的做法是，用 `any` 表示陣列中允许出现任意类型：

```ts
let list: any[] = ['Xcat Liu', 25, { website: 'http://xcatliu.com' }];
```

## 类陣列

类数组（Array-like Object）不是数组类型，比如 `arguments`：

```ts
function sum() {
    let args: number[] = arguments;
}

// index.ts(2,7): error TS2322: Type 'IArguments' is not assignable to type 'number[]'.
//   Property 'push' is missing in type 'IArguments'.
```

事实上常见的类陣列都有自己的接口定义，如 `IArguments`, `NodeList`, `HTMLCollection` 等：

```ts
function sum() {
    let args: IArguments = arguments;
}
```

关于内置对象，可以参考[内置对象](./built-in-objects.md)一章。

## 参考

- [Basic Types # Array](http://www.typescriptlang.org/docs/handbook/basic-types.html#array)（[中文版](https://zhongsp.gitbooks.io/typescript-handbook/content/doc/handbook/Basic%20Types.html#数组)）
- [Interfaces # Indexable Types](http://www.typescriptlang.org/docs/handbook/interfaces.html#indexable-types)（[中文版](https://zhongsp.gitbooks.io/typescript-handbook/content/doc/handbook/Interfaces.html#数组类型)）

---

- [上一章：对象的类型——接口](type-of-object-interfaces.md)
- [下一章：函数的类型](type-of-function.md)
