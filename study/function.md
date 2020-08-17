## 函数

#### 函数的参数以及返回值

```ts
//   参数要指定类型、返回值也要指定类型
function getTotal(one: number, two: number): number {
  return one + two;
}
const total = getTotal(1, 2);

//没有返回值的函数，我们就可以给他一个类型注解void，代表没有任何返回值。
//如果这样定义后，再加入任何返回值，程序都会报错。
function sayHello(): void {
  console.log("hello world");
}
//如果一个函数是永远也执行不完的，就可以定义返回值为never（执行的时候，抛出了异常，这时候就无法执行完了）
function errorFuntion(): never {
  throw new Error();
  console.log("Hello World");
}
//一直循环，也是我们常说的死循环，这样也运行不完
function forNever(): never {
  while (true) {}
  console.log("Hello JSPang");
}
```
```ts
//如果参数是对象---对象解构
function add({ one, two }: { one: number, two: number }): number {
  return one + two;
}
const three = add({ one: 1, two: 2 });
```