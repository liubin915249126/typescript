## class

#### 定义一个类
```ts
class Lady {
    content = "Hi，帅哥";
    sayHello() {
        return this.content;
    }
}
// 实例类的对象
const goddess = new Lady();
console.log(goddess.sayHello());
```
```ts
// 定义一个类
class Lady {
    content = "Hi，帅哥";
    sayHello() {
        return this.content;
    }
}
// XiaoJieJie类身上既有自己的方法，也有从Lady类继承来的方法
class XiaoJieJie extends Lady {
    sayLove() {
        return "I love you";
    }
}
console.log(new XiaoJieJie().sayHello());//Hi，帅哥
console.log(new XiaoJieJie().sayLove());//I love you
```

#### 类的访问类型 --- private、protected、public
- public
  public从英文字面的解释就是公共的或者说是公众的，在程序里的意思就是允许在类的内部和外部被调用.
- private
  private 访问属性的意思是，只允许再类的内部被调用，外部不允许调用
- protected
 protected 允许在类内及继承的子类中使用

 #### enum
 ```ts
 enum Stauts {
    ZERO,
    ONE,
    TWO,
};
```
