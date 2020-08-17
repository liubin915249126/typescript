####
泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

####
将泛型当作变量
```ts
function identity2<T>(arg:T[]):T[]{
    //这里是将函数参数的所有元素的类型提升为泛型，并且将泛型作为返回数组的类型
    console.log(arg.length)
    return arg
}
```
在函数中使用泛型
```ts
function identity<T, Y, P>(first: T, second: Y, third: P): Y {
  return second
}
// 指定类型
identity<boolean, string, number>(true, '字符串', 123) // 字符串
// 类型推断
identity('string', 123, true) // true

```
在类中使用泛型
```ts
class DataManager<T> {
  // 定义一个类，该类中具有一个T类型的私有数组
  constructor(private data: T[]) {}
  // 根据索引说数组中的值
  getItem(index: number): T {
    return this.data[index]
  }
}
const data = new DataManager(['一碗周'])
data.getItem(0) // 一碗周
```
泛型还可以继承与于某个接口
```ts
interface Item {
  name: string
}
class DataManager<T extends Item> {
  // 定义一个类，该类中具有一个T类型的私有数组
  constructor(private data: T[]) {}
  // 根据索引说数组中的值
  getItem(index: number): string {
    return this.data[index].name
  }
}
const data = new DataManager([{ name: '一碗周' }])
data.getItem(0) // 一碗周

```
泛型约束中使用类型参数
```ts
// 定义一个接口
interface Person {
  name: string
  age: number
  hobby: string
}
// 定义一个类
class Me {
  constructor(private info: Person) {}
  getInfo(key: string) {
    return this.info[key]
  }
}
const me = new Me({
  name: '一碗周',
  age: 18,
  hobby: 'coding',
})
// 调用 me.getInfo() 可能会得到一个 undefined 如下示例
me.getInfo('myName') // undefined

// 解决办法 
class Me {
  constructor(private info: Person) {}
  // 该写法与如下写法是一样的
  getInfo<T extends keyof Person>(key: T): Person[T] {
    return this.info[key]
  }
  // getInfo<T extends 'name' | 'age' | 'hobby'>(key: T): Person[T] {
  //     return this.info[key]
  // }
}
const me = new Me({
  name: '一碗周',
  age: 18,
  hobby: 'coding',
})
// 调用 me.getInfo() 如果传递一个未知的属性则会编译错误
me.getInfo('myName') // error : 类型“"myName"”的参数不能赋给类型“keyof Person”的参数。

```