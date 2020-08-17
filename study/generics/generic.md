## 范型
泛型：[generic - 通用、泛指的意思],那最简单的理解，泛型就是泛指的类型。
泛型的本质是参数化类型，通俗的将就是所操作的数据类型被指定为一个参数，
这种参数类型可以用在类、接口和方法的创建中，分别成为泛型类，泛型接口、泛型方法。
泛型的定义使用<>（尖角号）进行定义

```js
// identity函数。 这个函数会返回任何传入它的值
// function identity(arg: number): number {
//     return arg;
// }
// 这时identity函数就不可以传除number类型以外类型的参数
// console.log(identity(1))

// function identity(arg: any): any {
//     return arg;
// }
// // 使用any类型会导致这个函数可以接收任何类型的arg参数，
// // 这样就丢失了一些信息：传入的类型与返回的类型应该是相同的（要自己typeof才会知道）
// console.log(identity(111))

// 泛型的使用
function identity<T>(arg: T): T {
    return arg;
}
console.log(identity(111))

//STR：两个参数的类型相同
function join<STR>(first: STR, second: STR) {
    return `${first}${second}`;
}
// 参数的类型可以在调用的时候定义
console.log(join<string>("我是", "huahua"))//我是huahua
console.log(join<number>(1,2))//12
```

```ts
// class Person {
//     constructor(private girls: string[]) {}
//     getGirl(index: number): string {
//         return this.girls[index]
//     }
// }
// const girls = new Person(["huahua", "dahua", "xiaohua"]);
// console.log(girls.getGirl(1));//dahua
//此时若需要传入的数组是number类型的，上述代码则不能正常运行，此时使用泛型
class Person<T> {
    constructor(private girls: T[]) {}
    getGirl(index: number): T {
        return this.girls[index]
    }
}
const girls = new Person<string>(["huahua", "dahua", "xiaohua"]);
const boys = new Person<number>([1,2,3])
console.log(girls.getGirl(1));//dahua
console.log(boys.getGirl(1));//2
```
```ts
interface Girl {
    name: string
}
class Person<T extends Girl> {
    constructor(private girls: T[]) { }
    getGirl(index: number): string {
        return this.girls[index].name
    }
}
const girls = new Person([
    { name: "huahua" },
    { name: "dahua" },
    { name: "xiaohua" },
]);
console.log(girls.getGirl(1));//dahua
```