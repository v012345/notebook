### 安装ts的编译器
```console
npm i -g typescript
```
### 编译
```console
tsc tsFileName.ts
```

### 类型声明
```TypeScript
let a : number;
a = 123;
let b : number = 123;
let c = 123; // 自动给c加上number类型
```

|  类型   |
| :-----: |
| number  |
| string  |
| boolean |
| 字面量  |
|   any   |
| unknown |
|  void   |
|  never  |
| object  |
|  array  |
|  tuple  |
|  enum   |


```TypeScript
// 字面量用法
let a: 10;//那就a就是10
a = 10; //可以
a = 11; //不可以
let b: "male" | "female";
b = "male"; //可以
b = "female"; //可以
b = "boy"; //不可以
```
```TypeScript
// | 的用法(联合类型)
let a: number | string;
a = 10; //可以
a = "hi"; //可以
a = true; //不可以
```
```TypeScript
let a: any;
let b;
// a 和 b 随便什么都行,相当于关闭了TS的类型检测
// b 是解析器自动给上的any
b = "hi";
let c: number;
c = b; //可以,any可以赋值给任何类型,非常的不好
```
```TypeScript
let a: unknown;
a = "hi"; //可以
a = 10; //可以
let b: number;
b = a; //会警告,相当于把unknown赋给了string;

if(typeof a === "number") b = a; //可以,没有警告了
// or
b = a as number; //手动告诉解析器(类型断言),a就是number类型,没问题的
b = <number> a; //同上
```
```typescript
function a():void{} // 没有返回值
```
```typescript
function a():never{ // 真的什么都不返回!!还void都不是
    throw new Error('bug!');
}
```







