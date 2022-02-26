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
```ts
let a: object;
let a = {}; //一般不这么用,没意思

let b: {id: number, name?: string}; //name可选
b = { id: 1 }; //这么用

let c: {id: number, [key: string]:any };
c = {id: 1, name: "c" , age: 18}; //[key: string]:any 就表示任意啦
```
```ts
// 类似object , 还有Function ,虽上面总类型中没有列出来
let a: Function; // 没什么意思
let b: (a:number , b:number) => boolean; // 用类似箭头函数的形式,指明参数与返回值
b = function (n1:number,n2:number):boolean{
    return n1 >= n2
}
```
```ts
// 数组
let a: string[]; // 字符串数组
let b: Array<string>; // 同上
```
```ts
// tuple, 就是固定长度的数组, 效率上好一些
let a: [string,string,number];
a = ["a","b",123];
```
```ts
// enum, 默认为0,1,2,当然也可以自己定,一般就对应数字
enum Gender { Male, Female, Other = "fff" };
console.log(Gender.Male); //0
```
```ts
// & ,和 | 对应
let a : string & number; // 这样没什么意义,但是下面的
let b : { id:number } & { name:string }; // 表示两个都要有
let b = { id : 1, name: "b"};
```
```ts
// type 关键字,自定义类型
type T = 1| 2| 3| 4; //1-4的字面量
let a:T;
a = 1; // ok
a = 5; // no
```

### 编译选项
加上`-w`参数,会启动监视模式,监视指定文件,进行"实时"编译
```console
tsc fileName.ts -w
```
上面的方式,对整体项目来说,有点不实用.

另一种方式
在项目根目录生成`tsconfig.json`文件

`/tsconfig.json`
```json
{

}
```
之后运行
```console
tsc
```
会对整个项目进行编译.

运行
```console
tsc -w
```
会对整个项目进行监视,实时编译

下面讲讲`tsconfig.json`具体的的配置项
```json
{
    
    // 指定哪些ts文件需要被编译
    // 比如, "./scr/**/*", 注意 ** 指任意路径, * 指任意文件,所以这个下, 当前scr目录下的任意目录的任意文件
    //
    //
    
    "include":["./scr/**/*"],

    // 排除指定文件
    // 默认值为 ["node_modules","bower_modules","jspm_modules"] , 所以一般这个选项都不用设置.
    "exclude":[],

    // 引入一个外引配置文件
    // 引入 configs下的base.json中的所有配置信息
    "extends":"./configs/base",

    // 指定要编译的文件,一般文件少时才用到,和include有点像
    // 一般用不到
    "files":["app.ts","view.ts"],

    /**
    * 编译器选项,很重要
    */
    "compilerOptions": {
        // 指定被编译为的ES版本,想看全部参数,就给个错误值,报错信息里有
        "target": "es2015",

        // 指定要使用的模块化的规范,看全部参数的方法同上
        "module": "es2015",

        // 指定项目要用的库,一般不写出来,注掉,用默认就好,看全部参数的方法同上
        "lib":[],

        // 用来指定编译后文件所在的目录,我不知道会不会保留目录结构
        "outDir":"./dist",

        //将代码合并为一个文件输出,所有的全局作用域中的代码会合并到同一个文件中,注意,模块化是不好合并的,只支持"module"为"system" or "amd" 的规范时才行,所以这个配置一般也不用,注掉就行,回合的工作,让打包工具去做
        "outFile":"./dist/app.js",

        // 是否编译 include 里的 js 文件, 默认为不编译
        "allowJs": false,

        // 是否也检查 js 文件的代码规范, 默认为不检查
        "checkJs": false,

        // 是否连同注释一起编译,默认为一起编译
        "removeComments": false,

        // 不生成编译后的文件,默认为生成,如果不生成,一般只用来检查代码是否会在编译环节出问题.
        "noEmit":false,

        // 当编译发生错误时,不生成编译后的文件,默认为生成
        "noEmitOnError":false,

        // 严格检查的总开关,可以设为 true ,之后分项去关
        "strict":true,

        // 严格模式,开启的话,就是比较严格,但性能上好一些,默认不开
        "alwaysStrict":true,

        // 如果不开的话,代码定义变量时,如果不写类型,就自动定义成 any ,这样不好,所以开启这个, 必须写上类型,就算是 any 也要手动写上
        "noImplicitAny":true,

        // 不允许不明确类型的this, 由于在 function 中 ,this 会因为不同的调用方式,指向不同的东西,一会是 Window 一会是对象,所以现在必须显式的指用这个this的类型.如, function f(this:Window){console.log(this);}
        "noImplicitThis":true,

        // 严格检查空值,有的时候,比如 getElementById 之类,会返回null,这个时候如果直接使用返回值就会报错,所以要先,用 if(a !== null){...} 或者 a?.someMethod() 的方法 我还是第一次知道这个?的写法
        "strictNullChecks":true,
    }
}
```
### class
```ts
class Cat{
    color:string;
    static BREED:string = "Dragon Li";// 可以和 readonly 连和 static readonly preporty: type = ??;
    readonly owner: string = "No One"; // 类型 final
    constructor(c:string){
        this.color = c
    }
    poop(){
    }
}
```
### extends
```ts
class A {}
class B extends A{}
```

### super
```ts
class A {
    a:string;
    constructor(a:string){this.a = a}
    f(){}
}


class B extends A{
    b:string;
    constructor(a:string,b:string){
        super(a);
        this.b = b
    }
    m(){
        super.f();
    }
}
```

### abstract
```ts
abstract class A {
    a:string;
    constructor(a:string){this.a = a}
    abstract f():void
}


class B extends A{
    b:string;
    constructor(a:string,b:string){
        super(a);
        this.b = b
    }
    f(){}
}
```

### interface
可以代替关键字`type`使用,注意";",当然还有高级用法啦  
可以"重名",相当把两个合一起去实现
```ts
interface I {
    name:string;
}
interface I {
    age: number;
}
const o:I = {
    name:"123",
    age:10
}
```
接口和抽象类很像,区别是接口中的属性不能在初始值,方法不能有方法体,抽象类的属性可以在初始值
```ts
interface I {
    name: string;
    poop():void;
}
class Human implements I {
    name: string;
    constructor(n){this.name = n}
    poop(){}
}
```

### public , private , protected
先说一下 `getter` 和 `setter`, 除了可以手动写 getter 和 setter 外, 还可以这样
```ts
class A {
    private _age : number = 10;
    get age(){ return this._age } //我没试 不加_的情况
    set age(age:number){ this._age = age }
}
let a = new A();
console.log(a.age); // 10
a.age = 11;
console.log(a.age); // 11
```
一个语法糖
```ts
class A {
    constructor(public age:number){}
}
let a = new A(10);
console.log(a.age); //10
```

### 泛型
"广泛的类型",英文是什么我不知道
```ts
function f<T>(a:T):T{
    return a;
}
f(10); //10
f<string>("123"); //123
// 上面两条是简单用法,我比较喜欢第二个
// 还可以 extends 接口 或者 类
interface I {
    name:string;
}
class C {
    age:number;
}
function fn<T extends I, K extends C>(a:T,b:K):void{}

class A extends C implements I {
    name:string = "A";
    age:number = 10;
}

new a = new A();

fn<A,A>(a,a);
```
创建类时也可以用泛型
```ts
class A<T>{
    name:T;
    constructor(name:T){ this.name = name; }
}
let a = new A<string>("a");
```





