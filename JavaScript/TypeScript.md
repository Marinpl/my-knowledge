> **TypeScript基础**

# 一、入门

## 0、安装TypeScript

## 1、基础知识

## 2、类型

#### 1、类型声明

可以给变量指定类型，指定该变量的类型(类java)

```typescript
// 声明变量a，指定类型number
let a: number;
// 联合类型(&)
let a: number | string ;
// 变量的声明和赋值同时进行时，会进行类型检测
let b = true;
// 函数中参数和返回值也可以声明
// 将sum方法中参数和返回值声明为数值类型
function sum(a: number,b: number): number{
    return a+b;
}
// 使用类似箭头函数表达
let javaC: (a,b) => 1;
let c: (a: number,b: number): number=>1;
// 等同于
let c = function(a: number,b: number): number{
    return 1;
}

```

#### 2、类型一览

| 类型    | 例子               | 描述                         |
| ------- | ------------------ | ---------------------------- |
| number  | 1，-2，3.4         | 任意数字                     |
| string  | "pig"              | 任意字符串                   |
| boolean | true，false        | true或false                  |
| 字面量  | 本身               | 限制变量的值就是该字面量的值 |
| any     | 自身关闭ts类型检测 | 任意类型(不安全)             |
| unknown |                    | 类型安全的any                |
| void    | 空值(undefined)    | undefined或null              |
| never   | 没有值             | 不能是任何值                 |
| object  | {name:"pig"}       | 任意JS对象                   |
| array   | [1,2,3]            | 任意JS数组                   |
| tuple   | [4,5]              | 固定长度数组                 |
| enum    | enum{A,B}          | 枚举                         |
| type    |                    | 简化类型别名                 |

```typescript
// 字面量声明联合类型
let a: "male" | 123;
// any和unknown
// 避免显示any和隐式any(不声明类型默认即为any)
let b1: unknown;
let b2: unknown | number;
b = "hello"; // 成立
b = 123 // 成立

//通过类型判断或断言，无法直接通过unknown类型赋值
let c: string;
c = b1;  //报错
// 类型判断
if(typeof b1 === string){
    c = b1;
}
// 断言
c = b1 as string;
c = <string>b1

// never
function fn1(): never{
    throw new Error("!")
}

// object
// 在属性名后加?，表示可选属性
let e: {name: string,age?: number};
e = {name: "pig",age: 123}
// 后面属性不限制，使用[自定义变量名:string]:类型
let e: {name: string,[自定义变量名:string]:any};
e = {name: "pig",age: 123,gender: "male"}

// 数组和元组
let e :number[];
let f :Array<number>;
let g :[string,string]

// 枚举
enum H{
    name = "老王"
}
function getHName(name:H){
    name = H.name
}
```

## 3、编译选项

#### 1、命令行编译

**TS编译要通过tsc xxx.ts转换为JS，才能在页面上使用**

```bash
# 将test.ts 转换为 test.js
$ tsc test.js
# 将test.ts 转换为 test.js并开始监视
$ tsc test.js -w
```

#### 2、tsconfig.json配置

**新建tsconfig.json文件，可以编译所有TS文件而不用逐个编译**

```typescript
// tsconfig.json文件样式
{
	// "存放相关配置"
}
```

>**include，exclude，files**

-----用来指定哪些TS文件需要或不需要编译

```typescript
"include":["TS文件路径"]

"exclude":["TS文件的路径"]   // exclude默认值为node_modules,bower_components,jspm_packages

"files":["文件名","文件名"...]
// 例子:编译src目录下的所有目录**的所有文件*
"include":["./src/**/*"]
```

>**extends**

------继承配置文件，将其他配置文件合并

```typescript
// 例子:将config下的base配置合并到tsconfig.json文件中
"extends":["./config/base"]
```

>**compilerOptions**

------详细配置与各个子选项作用

```typescript
// 编译器版本配置，下面括号内容可通过错误提示查看所有版本
"target":"指定转换的js版本(es2015)",     
"module":"指定使用的模块化规范(es6)",
"lib":[指定项目中要使用的库(esnext.promise)],          //node中使用较多
    
// 编译器编译配置
"outdir":"指定编译后的js文件位置",
"outfile":"将编译后的所有全局作用域js文件合并到一个文件中"   //模块化只能使用amd和system
"allowJS":false/true,                                //是否对已有js文件进行编译，默认为false
"checkJs":false/true,								 //检察js语法是否符合ts规范，默认为false
"removeComments":true/false,						 //是否编译注释，默认为true
"noEmit":false/true,								 //生成编译文件，默认为false
"noEmitOnError":false/true,							 //当有错误时，不生成编译文件，默认为false
     
// 编译器检察配置
"strict":false/true									//所有严格检察全部开启or关闭，默认为false
"alwaysStrict":false/true,							//编译后的js文件使用严格模式，默认为false
"noImplicitAny":false/true,							//不允许任何显示隐式any，默认为false
"noImplicitThis":false/true,						//检察不明确类型this，默认为false
"strictNullChecks":false/true,						//严格检察空值，默认为false
```

## 4、使用打包工具打包ts文件

### 使用Webpack



### 使用Vite



# 二、面向对象

## 0、什么是面向对象

编程是对现实种种概念的抽象，对象就是将不同状态，不同量词的物质抽象：一个人，一辆车，一个分子，跑，飞，跳等等。

面向对象即通过对象进行一系列的操作，含有的属性以及方法都是从对象为出发点的。

## 1、类

定义类：

```typescript
class 类名{
    属性名:类型;
    
    constructor(参数:类型){
        ....
    }
    
    方法名(){
        ....
    }
}

// 访问类中属性，需要定义实例xxx
const xxx = new 类名();
```

## 2、重要语法

>**静态属性(类属性) static**

无需创建对象，直接访问类即可

```typescript
class StaticClass{
	static test1 : string = "哈哈"
}
StaticClass.test1;  //哈哈
```

>**构造函数 constructor**

初始化(赋值)相关属性。构造函数会在创建对象时调用，可以通过this向新建对象添加属性

```typescript
class 类名{
    constructor(参数1: 类型,参数2: 类型){
        this.参数1 = 参数1;
        this.参数2 = 参数2
    }
}

const xxx = new 类名(参数1,参数2)
```

>**this**

在方法中，使用this表示当前调用方法的对象。在实例(构造函数)方法中，this就代表当前的实例

>**继承 extends**

类似java，通过extends继承，子类默认有父类属性，可以通过重写覆盖

```typescript
class Animal{
    name: string;
    constructor(name: string){
        this.name = name
    }
    sayHello(){
        console.log("动物会叫")
    }
}

class Dog extends Animal{
    sayHello(){
        console.log("汪汪汪")
    }
}

const dog = new Dog("旺财")
console.log(dog.name); //旺财
dog.sayHello();   // 汪汪汪
```

>**super**

直接调用父类方法super.父类方法或属性，如果子类有新的构造函数，使用super()调用父类的构造函数

>**抽象类 abstract**

通过关键字abstract，使父类无法创建对象

抽象方法在抽象类中抽象定义，没有方法体。在子类中具体实现

```typescript
abstract class Animal{
    name: string;
    abstract sayHello():void;
}
class Dog extends Animal{
    sayHello(){
        console.log("汪汪")
    }
}
```

>**接口 interface** 

接口用来定义一个类中包含的所有具体属性和具体方法，用来进行类型声明

接口所有属性不能有实际值，方法都是抽象方法

```typescript
interface AnimalInter{
    name: string;
    sayHello():void;
}
class Dog implements AnimalInter{
    name: string;
    constructor(name: string){
        this.name = name;
    }
    sayHello(){
        console.log("汪汪")
    }
}
```

> **属性封装**

防止属性具体值被直接修改，使用private/protected/public关键字，属性名前加_，使用getter和setter方法调用

```typescript
// ts设置getter,setter方法
// 属性名前加_
class 类名(
    constructor(访问权限 _属性: 类型);
)
get 属性名(){
    return this._属性名
}
set 属性名(value:string){
    this._属性名 = value
}
```

> **泛型**

在定义函数或类时，遇到不明确类型可用泛型

```typescript
function fn<T>(a: T): T{
    return a;
}
// 调用
fn(10);
fn<string>('hello!')
```

