## Basic Types
* `boolean`
* `number`
* `number[]` `Array<number>`
* `[string, number]`
* `enum Color {Red, Green, Blue}`
* `any`
* `void`  [声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null](https://www.tslang.cn/docs/handbook/basic-types.html) 联合类型string | null | undefined　用在联合类型中
* `never` 总是没有返回值
* `<string>someValue`  `someValue as string`

## interface接口
TypeScript的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

简单例子
```js
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);

// 可选属性
interface SquareConfig {
  color?: string;
  width?: number;
}

// 只读属性
interface Point {
    readonly x: number;
    readonly y: number;
}


```
把整个ReadonlyArray赋值到一个普通数组也是不可以的。 但是你可以用类型断言重写：

`a = ro as number[];`

### 函数类型
```js
interface SearchFunc {
  (source: string, subString: string): boolean;
}
```

### 可索引的类型
```js
interface StringArray {
  [index: number]: string;
}
```

## 类型注解
TypeScript里的类型注解是一种轻量级的为函数或变量添加约束的方式。


## 泛型
软件工程中，我们不仅要创建一致的定义良好的API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

在像C#和Java这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。

```js
function identity(arg: any): any {
    return arg;
}
```
使用any类型会导致这个函数可以接收任何类型的arg参数，这样就丢失了一些信息：传入的类型与返回的类型应该是相同的。如果我们传入一个数字，我们只知道任何类型的值都有可能被返回。

因此，我们需要一种方法使返回值的类型与传入参数的类型是相同的。 这里，我们使用了 类型变量，它是一种特殊的变量，只用于表示类型而不是值。
```js
function identity<T>(arg: T): T {
    return arg;
}
```