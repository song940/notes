---
title: TypeScript
layout: default
parent: JavaScript
---

# TypeScript

**TypeScript 入门指南**

欢迎来到 TypeScript 入门指南！TypeScript 是一种 JavaScript 的超集，添加了可选的静态类型和基于类的面向对象编程。

**1. 为什么使用 TypeScript?**
- 更好的类型安全。
- 对现代 JavaScript 功能的支持。
- 更强大的工具和编辑器支持。
- 更好的协作。

**2. 安装 TypeScript**

要开始使用 TypeScript，首先你需要安装它。

```shell
npm install -g typescript
```

**3. 编写你的第一个 TypeScript 文件**

创建一个名为 `hello.ts` 的文件：

```typescript
function sayHello(name: string): void {
    console.log(`Hello, ${name}!`);
}

sayHello('TypeScript');
```

注意我们是如何添加类型注释的，这是 TypeScript 的一个特点。

**4. 编译 TypeScript 文件**

使用 TypeScript 编译器 (`tsc`) 来编译上面的文件：

```shell
tsc hello.ts
```

这将生成一个 `hello.js` 文件，你可以像普通的 JavaScript 文件那样运行它。

**5. 基本类型**

TypeScript 包括以下基本类型：

- `boolean`: 例如 `let isDone: boolean = false;`
- `number`: 例如 `let decimal: number = 6;`
- `string`: 例如 `let color: string = "blue";`
- `array`: 例如 `let list: number[] = [1, 2, 3];`
- `tuple`: 例如 `let x: [string, number] = ['hello', 10];`
- `enum`: 例如 `enum Color {Red, Green, Blue}`
- `any`: 用于那些类型不确定的变量
- `void`: 通常用于没有返回值的函数的返回类型

**6. 接口**

接口是 TypeScript 的一个核心原则，它可以用来定义对象的形状。

```typescript
interface Person {
    firstName: string;
    lastName: string;
}

function greet(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Tom", lastName: "User" };

console.log(greet(user));
```

**7. 类**

TypeScript 支持基于类的面向对象编程。

```typescript
class Greeter {
    greeting: string;

    constructor(message: string) {
        this.greeting = message;
    }

    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```

**8. 模块**

当应用规模变大时，模块可以帮助组织代码。你可以像下面这样导入和导出模块：

```typescript
// math.ts
export function add(x: number, y: number): number {
    return x + y;
}

// main.ts
import { add } from './math';

console.log(add(1, 2));
```

**9. 更多资源**

- [官方文档](https://www.typescriptlang.org/docs/)
- [TypeScript Deep Dive](https://basarat.gitbooks.io/typescript/)

---

开始使用 TypeScript 可能需要一些时间来适应，特别是如果你之前只使用过 JavaScript。但随着时间的推移，你会发现 TypeScript 提供的类型安全和其他功能非常有价值。