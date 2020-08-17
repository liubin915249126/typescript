## TS 数据类型

#### 基础静态类型
null,undefinded,symbol,boolean,void,any这些都是最常用的基础数据类型
```ts
    let count: number = 1;
    //这是一个number类型的
```

#### 对象类型
```ts
//  obj
const xiaoJieJie: {
  name: string,
  age: number,
} = {
  name: "大脚",
  age: 18,
};
console.log(xiaoJieJie.name);
// arr
const xiaoJieJies: String[] = ["谢大脚", "刘英", "小红"];
// class
const dajiao: Person = new Person();
// fun
const jianXiaoJieJie: () => string = () => {
  return "大脚";
};
// 自定义对象类型
interface XiaoJieJie {
  uname: string;
  age: number;
}
const xiaohong: XiaoJieJie = {
  uname: "小红",
  age: 18,
};
```

#### 数组
```js
const numberArr = [1, 2, 3];
//如果你要显示的注解，也非常简单，可以写成下面的形式。
const numberArr: number[] = [1, 2, 3];
//如果你的数组各项是字符串，你就可以写成这样。
const stringArr: string[] = ["a", "b", "c"];
//也就是说你可以定义任意类型的数组，比如是undefined。
const undefinedArr: undefined[] = [undefined, undefined];
//既有数字类型，又有字符串的时候
const arr: (number | string)[] = [1, "string", 2];
```
```ts
// 对象数组
const xiaoJieJies: { name: string, age: Number }[] = [
  { name: "刘英", age: 18 },
  { name: "谢大脚", age: 28 },
];

//上面的写法太麻烦，修改后
type Lady = { name: string, age: Number };

const xiaoJieJies: Lady[] = [
  { name: "刘英", age: 18 },
  { name: "谢大脚", age: 28 },
];

//上述写法在对象里再加入一个属性，编译器就会报错，修改为用类来定义
class Madam {
  name: string;
  age: number;
}

const xiaoJieJies: Madam[] = [
  { name: "刘英", age: 18 },
  { name: "谢大脚", age: 28 },
];
```

#### 元组
```ts
const xiaojiejie: (string | number)[] = ["dajiao", 28, "teacher"];
//调换数组中元素的位置，如下，ts不能检测到问题
const xiaojiejie: (string | number)[] = ["dajiao", "teacher", 28];
//这时，需要元祖来加强
const xiaojiejie: [string, string, number] = ["dajiao", "teacher", 28];
//把数组中的每个元素类型的位置给固定住了，这就叫做元组。
```

#### interface 接口的理解和使用
个人理解： 从js的角度看ts中的interface，就是先声明了一个对象obj，这个对象obj里面有很多的属性name，这个对象obj会在你后面定义的方法fun中当作参数（形参）传进去，这个对象obj中的属性有必传的、非必传的、还有函数类型的。你在方法fun中若要使用某个属性name，那么这个属性name需要在对象obj中定义过，否则会报错。(除非interface中定义了[propname: string]: any;属性)
注意：对象中的每一个属性都需要定义类型，方法定义返回值的类型
```ts
// 这是定义的一个obj
interface Girl {
    // 每一个属性都要有类型
    name: string;
    age: number;
    // 必传的属性
    height: number;
    // 非必传的属性
    footer?: number;
    // 允许加入任意值 
    // 在实参中新增了sex属性，interface中并没有定义，此时并没有报错
    [propname: string]: any;
    // 存方法，要定义返回值的类型
    say(): string;
    //非必传方法
    run?(): void;
}
// 后面定义的方法 fun 把上面定义的对象 Girl 当作参数传给方法
const screenResume = (girl: Girl) => {
    girl.age < 24 && girl.height >= 168 && console.log(girl.name + "进入面试");
    girl.age > 24 || (girl.height < 168 && console.log(girl.name + "你被淘汰"));
  };
  
  const getResume = (girl: Girl) => {
    console.log(girl.name + "年龄是：" + girl.age);
    console.log(girl.name + "身高是：" + girl.height + "cm");
    girl.footer  &&  console.log(girl.name + "鞋码是：" + girl.footer + "码");
    girl.sex && console.log(girl.name + "性别是：" + girl.sex);
    console.log(girl.name + "开心说：" + girl.say());
  };
  //实参
  const girl = {
    name: "大脚",
    age: 18,
    height: 174,
    footer: 38,
    // 这里不报错的原因是 interface中增加了 [propname: string]: any;属性
    sex: '女',
    say() {
        return "hello world";
      },    
  };
  //调用方法
  screenResume(girl);
  getResume(girl);
```
接口（interface）的引用（被class引用）
```ts
// implements 是指 类 引用了 某个 接口（interface）
//这里是指 XiaoJieJie这个类 引用了 Girl 这个接口，此时定义XiaoJieJie这个类的时候，要给必传属性赋值
class XiaoJieJie implements Girl {
    name = '小花';
    age = 18;
    height = 180;
    say() {
        return "傻子"
    }
}
//new XiaoJieJie() ----实例对象
screenResume(new XiaoJieJie())
getResume(new XiaoJieJie())
```