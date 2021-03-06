[![Twitter](https://img.shields.io/badge/twitter-@qq393464140-blue.svg)](http://twitter.com/qq393464140)

# es6-programme-style
> ECMAScript 6 编程风格

<a name="目录"></a>
## 目录

* [前言](#前言)
* [let 命令](#let)
* [const 命令](#const)
* [变量解构赋值](#变量解构赋值)
* [字符串模板](#字符串模板)
* [标签模板](#标签模板)
* [指数运算符](#指数运算符)
* [函数参数默认值](#函数参数默认值)
* [rest 运算符](#rest)
* [扩展运算符](#扩展运算符)
* [箭头函数](#箭头函数)
* [函数绑定运算符](#函数绑定运算符)
* [对象简洁表示法](#对象简洁表示法)
* [属性名表达式](#属性名表达式)
* [方法简洁表示法](#方法简洁表示法)
* [对象的扩展运算符](#对象的扩展运算符)
* [Generator 函数](#Generator)
* [Async 函数](#Async)
* [Class](#Class)
* [修饰器](#修饰器)
* [模块](#模块)
* [参考链接](#参考链接)
* [License](#License)

<a name="前言"></a>
## 前言 [🔝](#目录)

这是一遍关于 `ECMAScript 6`（以下简称 ES6）编程风格的文章。
如果你还没有了解 ES6，可以从这里开始[《ECMAScript 6 入门》]。

> 代码规范

众所周知，良好的`代码规范`会带来方方面面的好处。
但是，本篇文章不会重复讨论诸如[大括号的圣战]或者[缩进圣战]这类的问题。
如果，你想了解更多`代码规范`的内容，可以阅读这里 [JavaScript 编码规范]。

> 编程风格

`编程风格`是什么？`编程风格`可以说是`代码规范`的子集，我们不会考虑变量命名等问题。
并且，在`约束`的程度上，以`建议使用`为主。
在一定程度上，与各个团队的`代码规范`形成互补，补充关于 ES6 的内容。

> 快速入门

并不是所有的浏览器能执行 ES6 的代码，但我们可以使用 [Babel Compiler] 进行代码转译。
或者，你可以直接使用 [LegoFlow] 马上体验。

> 星号

带星号的特性，并不是 ES6 的标准特性，它或许仅仅是 ES7 的一个提案，但至少 `Babel` 已经支持转译了，我们可以尝试使用它们，享受它们带来的便利。

## 约定 [🔝](#目录)

在阅读以下内容前，请谨记以下约定：

* 关于代码兼容性：
    * 这里仅考虑 `webkit` 与 `trident` 。
    * 以 IE8 为分水岭。
    * IE8 能执行该特性转译后的代码则标记： ![](ie_good.png)
    * IE8 不支持该特性转译后的代码则标记： ![](ie_bad.png)
    * 如果，你是移动端的开发者，则不需要在意以上标记。
    * 如果，你是 PC 端的开发者，那么标红的特性，则不建议使用。

* 关于建议使用的程度：
    * 推荐程度较高则标记： ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)
    * 推荐程度一般则标记： ![](star_fill.png) ![](star_fill.png) ![](star.png)
    * 推荐程度较低则标记： ![](star_fill.png) ![](star.png) ![](star.png)

* 关于特性的使用姿势：
    * 正确姿势：😁
    * 错误姿势：😭
    * 转译后抛出异常的错误信息: ❌
        * 便于定位问题与兼容处理

<a name="let"></a>
## let 命令 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 使用 `let` 替换 `var`

```js
// 😁
for (let i = 0; i < 3; i++) {
    setTimeout(function () {
        console.log(i);
    }, 100);
}
```

[→在线转译][01]

* `let` 不再具备 `var` 的`变量提升`

```js
// 😭
function test () {
    flag = true;
    // 其他代码
    let flag;
    if (flag) {
        // 预期执行的代码
    }
}
```

[→在线转译][02]

<a name="const"></a>
## const 命令 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 定义一个`复杂类型`作为常量时，它的属性是可以更改的

```js
// 😭
const obj = {
    value : true
};
obj.value = false;
if (obj.value) {
    // 预期执行的代码
}
console.log(obj);
```

<a name="变量解构赋值"></a>
## 变量解构赋值 [🔝](#目录)

#### 对象的解构赋值 ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)


* 解构接口数据

```js
// 😁
let { uid, username, avator } = data;
console.log(uid, username, avator);
```

[→在线转译][03]

#### 数组的解构赋值 ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star.png)

* 解构数组

```js
// 😁
let param = 'key=value';
let [key, value] = param.split('=');
```

```
// ❌
对象不支持“isArray”属性或方法
```

[→在线转译][04]

#### 交换变量 ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 交换变量

```js
// 😁
let min = 1;
let max = 0;
if (min > max) {
    [min, max] = [max, min];
}
```

[→在线转译][05]

#### 混合解构与嵌套解构 ![](ie_bad.png) ![](star_fill.png) ![](star.png) ![](star.png)

* 不建议不能一目了然的解构

```js
// 😭
let {
    uid,
    username,
    message : [
        message0,
        message1,
    ],
} = data;
```

[→在线转译][06]

<a name="字符串模板"></a>
## 字符串模板 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 使用`` ` ``替换`'`和`"`
* 不能使用`条件语句`和`循环语句`，但可以使用`三目运算符`和`函数`

```js
// 😁
let text = `
    name : ${ username }
    sex : ${ sex ? 'female' : 'male' }
    medal : ${ getMedal() }
`;
```

[→在线转译][07]

<a name="标签模板"></a>
## 标签模板 [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star.png)

* `标签模板`也是`函数`，在 `i18n` 或者 `helper` 情景下使用比较适合

```js
// 😁
function parse ( templates, ...params ) {
    let output = templates[0];
    let length = params.length;
    if (navigator.language == 'zh-CN') {
        // 显示中文内容
        for (let index = 0; index < length; index++) {
            output += params[index].zh + templates[index + 1];
        }
    } else {
        // 显示英文内容
        for (let index = 0; index < length; index++) {
            output += params[index].en + templates[index + 1];
        }
    }
    return output;
}
let text = parse`uid : ${ uid }, name : ${ username }, avator : ${ avator }`;
```

```
// ❌
对象不支持“freeze”属性或方法
```

[→在线转译][08]

<a name="指数运算符"></a>
## 指数运算符 * [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* `Math.pow` 的语法糖

```js
// 😁
let hundred = 10 ** 2;
```

[→在线转译][09]

<a name="函数参数默认值"></a>
## 函数参数默认值 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 相比 `name = name || ''` 更优雅与直观，并且更严谨

```js
// 😁
function setName ( name = '' ) {
  window.name = name;
}
```

[→在线转译][10]

<a name="rest"></a>
## rest 运算符 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 比`arguments`更灵活

```js
// 😁
function foo ( elem, ...params ) {
  // ...
  console.log(params);
}
```

[→在线转译][11]

<a name="扩展运算符"></a>
## 扩展运算符 [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 调用`函数`时，使用`扩展运算符`可以将一个`数组`，变为`参数序列`

```js
// 😁
console.log(...[1, 2, 3], ...document.scripts);
```

```
// ❌
对象不支持“isArray”属性或方法
```

[→在线转译][12]

<a name="箭头函数"></a>
## 箭头函数 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 减少 `function` 关键字的词频，提高编码效率
* `this` 与 `arguments` 关键字，由定义时的环境决定而不是调用的环境
* 再也不用因为 `setTimeout` 的 `this` 指向 `window` 而定义各种 `self`，`_this`，`that`

```js
// 😁
let image = new Image;
image.onload = function () {
    setTimeout(() => {
        // 指向 image 而不是 window
        console.log(this);
    },3000);
};
image.src = url;
```

[→在线转译][13]

* 需要获取调用时的环境的 `this` 的情况下，不使用`箭头函数`

```
// 😭
function main () {
    document.addEventListener('click', ( event ) => {
        // 预期是 document 而不是 window
        console.log(this);
    }, false);
}
main();
```

[→在线转译][14]

<a name="函数绑定运算符"></a>
## 函数绑定运算符 * [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 以`链式调用`的方式调用`函数`
* `babel` 需要开启 `Experimental` 才能支持

```js
// 😁
function set ( key, value ) {
  this[key] = value;
  return this;
}
console.log({}::set('uid', '123')::set('username', 'Max'));
```

[→在线转译][15]

<a name="对象简洁表示法"></a>
## 对象简洁表示法 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 当`变量`与`属性名`同名时，推荐简写合并，比如调用 `ajax` 时的传参，保持`变量`一致，提高代码可读性

```js
// 😁
let username = 'Max';
// 其他代码
let data = {
  username,
  avator,
};
```

[→在线转译][16]

<a name="属性名表达式"></a>
## 属性名表达式 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* `属性名`支持表达式

```js
// 😁
let id = 1024;
let obj = {
  ['prefix' + id] : id,
};
```

[→在线转译][17]

<a name="方法简洁表示法"></a>
## 方法简洁表示法 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 减少 `function` 关键字的词频，提高编码效率

```js
// 😁
let obj = {
  log ( ...args ) {
    console.log(...args);
  },
};
```

[→在线转译][18]

<a name="对象的扩展运算符"></a>
## 对象的扩展运算符 * [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 将一个`对象`的可遍历属性拷贝到其他`对象`，`Object.assign` 的语法糖

```js
// 😁
let animal = { foot : 4 };
let cat = { ...animal, tail : 1 };
```

[→在线转译][19]

<a name="Generator"></a>
## Generator 函数 [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star.png) ![](star.png)

* `Generator` 依赖 `regeneratorRuntime`，所以 `babel` 需要添加 `babel-plugin-transform-runtime` 插件

```js
// 😁
function* Genertor ( arg ) {
    // 同步代码，异步执行
    let input = yield arg;
    console.log(input);
    return 'end';
}

let genertor = Genertor('begin');

console.log(genertor.next().value);

console.log(genertor.next('input').value); // 外部注值
```

```
// ❌
缺少标识符、字符串或数字
```

<a name="Async"></a>
## Async 函数 * [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* `Generator` 的语法糖
* 因为依赖 `regeneratorRuntime`，所以 `babel` 需要添加 `babel-plugin-transform-runtime` 插件

```js
// 😁
import $ from 'jquery';

let getData = async ( url ) => {
    let data = await $.ajax(url);
    return data;
};

getData('http://legox.yy.com/mock/api/33').then(( data ) => {
    console.log(data);
});
```

```
// ❌
缺少标识符、字符串或数字
```

<a name="Class"></a>
## Class [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 比`构造函数更规范`，可读性更高

```js
// 😁
class Widget {

    constructor ( ...args ) {
        // ...
    }

    method () {
        // 方法
    }

    static foo () {
        // 类的静态方法
    }
}

class Pendant extends Widget {

    constructor ( ...args ) {
        super(...args);
        // 继承
    }

}

let pendant = new Pendant();
```

```
// ❌
对象不支持此操作
```

[→在线转译][20]

<a name="修饰器"></a>
## 修饰器 [🔝](#目录) ![](ie_bad.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* `babel` 需要开启 `Experimental` 才能支持

```js
// 😁
function readonly ( target, name, descriptor ){
    descriptor.writable = false;
    return descriptor;
}

class Person {
    @readonly
    name () {
        // ...
    }
}
```

```
// ❌
对象不支持此操作
```

[→在线转译][21]

<a name="模块"></a>
## 模块 [🔝](#目录) ![](ie_good.png) ![](star_fill.png) ![](star_fill.png) ![](star_fill.png)

* 使用 `import`，`export`

```js
// 😁
import $ from 'jquery';

export default {
    // ...
};
```

[→在线转译][22]

* `import` 将会 `提升` 到模块的头部

```js
// 😭
window.jQuery = require('$');

import 'jquery.parallax';
```

[→在线转译][23]

<a name="参考链接"></a>
## 参考链接 [🔝](#目录)

* [《ECMAScript 6 入门》]
* [JavaScript 编码规范]
* [Babel Compiler]
* [LegoFlow]
* [Babel 在线实验室]
* [ECMAScript 6 部署进度]

<a name="License"></a>
## License [🔝](#目录)

MIT

***
[《ECMAScript 6 入门》]: http://es6.ruanyifeng.com/
[大括号的圣战]: http://mp.weixin.qq.com/s?__biz=MzAxMzMxNDIyOA==&mid=215114843&idx=1&sn=5a765de3c9a0ab60ebe193eee09770f9&scene=21
[缩进圣战]: http://mp.weixin.qq.com/s?__biz=MzAxMzMxNDIyOA==&mid=215766844&idx=1&sn=59b52569b7c52ac874e0b2fdb4bce3f1&scene=21
[JavaScript 编码规范]: https://github.com/duowan/fe-guide/blob/master/javascript-guide.md
[Babel Compiler]: http://babeljs.io/
[LegoFlow]: http://legox.yy.com/legoflow/
[Babel 在线实验室]: http://babeljs.cn/repl/
[ECMAScript 6 部署进度]: http://kangax.github.io/compat-table/es6/
[01]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=for%20(let%20i%20%3D%200%3B%20i%20%3C%203%3B%20i%2B%2B)%20%7B%0A%20%20%20%20setTimeout(function()%7B%0A%20%20%20%20%20%20%20%20console.log(i)%3B%0A%20%20%20%20%7D%2C%20100)%3B%0A%7D
[02]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20test%20()%20%7B%0A%20%20%20%20flag%20%3D%20true%3B%0A%20%20%20%20%2F%2F%20%E5%85%B6%E4%BB%96%E4%BB%A3%E7%A0%81%0A%20%20%20%20let%20flag%3B%0A%20%20%20%20if%20(flag)%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E9%A2%84%E6%9C%9F%E6%89%A7%E8%A1%8C%E7%9A%84%E4%BB%A3%E7%A0%81%0A%20%20%20%20%7D%0A%7D
[03]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20%7B%20uid%2C%20username%2C%20avator%20%7D%20%3D%20data%3B%0Aconsole.log(uid%2C%20username%2C%20avator)%3B
[04]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20param%20%3D%20'key%3Dvalue'%3B%0Alet%20%5Bkey%2C%20value%5D%20%3D%20param.split('%3D')%3B
[05]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20min%20%3D%201%3B%0Alet%20max%20%3D%200%3B%0Aif%20(min%20%3E%20max)%20%7B%0A%20%20%20%20%5Bmin%2C%20max%5D%20%3D%20%5Bmax%2C%20min%5D%3B%0A%7D
[06]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20%7B%0A%20%20%20%20uid%2C%0A%20%20%20%20username%2C%0A%20%20%20%20message%3A%20%5B%0A%20%20%20%20%20%20%20%20message0%2C%0A%20%20%20%20%20%20%20%20message1%2C%0A%20%20%20%20%5D%2C%0A%7D%20%3D%20data%3B
[07]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20text%20%3D%20%60%0A%20%20%20%20name%3A%20%24%7B%20username%20%7D%0A%20%20%20%20sex%3A%20%24%7B%20sex%20%3F%20'female'%20%3A%20'male'%20%7D%0A%20%20%20%20medal%3A%20%24%7B%20getMedal()%20%7D%0A%60%3B
[08]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20parse%20(%20templates%2C%20...params%20)%20%7B%0A%20%20%20%20let%20output%20%3D%20templates%5B0%5D%3B%0A%20%20%20%20let%20length%20%3D%20params.length%3B%0A%20%20%20%20for%20(let%20index%20%3D%200%3B%20index%20%3C%20length%3B%20index%2B%2B)%20%7B%0A%20%20%20%20%20%20%20%20output%20%2B%3D%20params%5Bindex%5D%20%2B%20templates%5Bindex%20%2B%201%5D%3B%0A%20%20%20%20%7D%0A%20%20%20%20return%20output%3B%0A%7D%0Alet%20text%20%3D%20parse%60uid%3A%20%24%7B%20uid%20%7D%2C%20name%3A%20%24%7B%20username%20%7D%2C%20avator%3A%20%24%7B%20avator%20%7D%60%3B
[09]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20hundred%20%3D%2010%20**%202%3B
[10]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20setName%20(%20name%20%3D%20''%20)%20%7B%0A%20%20document.querySelector('%23name').innerText%20%3D%20name%3B%0A%7D
[11]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20foo%20(%20elem%2C%20...params%20)%20%7B%0A%20%20%2F%2F%20...%0A%20%20console.log(params)%3B%0A%7D
[12]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=console.log(...%5B1%2C%202%2C%203%5D%2C%20...document.scripts)%3B
[13]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20image%20%3D%20new%20Image%3B%0Aimage.onload%20%3D%20function%20()%20%7B%0A%20%20%20%20setTimeout(()%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E6%8C%87%E5%90%91%20image%20%E8%80%8C%E4%B8%8D%E6%98%AF%20window%0A%20%20%20%20%20%20%20%20console.log(this)%3B%0A%20%20%20%20%7D%2C3000)%3B%0A%7D%3B%0Aimage.src%20%3D%20url%3B
[14]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20main%20()%20%7B%0A%20%20%20%20document.addEventListener('click'%2C%20(%20event%20)%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E9%A2%84%E6%9C%9F%E6%98%AF%20document%20%E8%80%8C%E4%B8%8D%E6%98%AF%20window%0A%20%20%20%20%20%20%20%20console.log(this)%3B%0A%20%20%20%20%7D%2C%20false)%3B%0A%7D%0Amain()%3B
[15]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=function%20set%20(%20key%2C%20value%20)%20%7B%0A%20%20this%5Bkey%5D%20%3D%20value%3B%0A%20%20return%20this%3B%0A%7D%0Aconsole.log(%7B%7D%3A%3Aset('uid'%2C%20'123')%3A%3Aset('username'%2C%20'Max'))%3B
[16]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=let%20username%20%3D%20'Max'%3B%0A%2F%2F%20%E5%85%B6%E4%BB%96%E4%BB%A3%E7%A0%81%0Alet%20data%20%3D%20%7B%0A%20%20username%2C%0A%20%20avator%2C%0A%7D%3B
[17]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=let%20id%20%3D%201024%3B%0Alet%20obj%20%3D%20%7B%0A%20%20%5B'prefix'%20%2B%20id%5D%20%3A%20id%2C%0A%7D%3B
[18]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=let%20obj%20%3D%20%7B%0A%20%20log%20(%20...args%20)%20%7B%0A%20%20%20%20console.log(...args)%3B%0A%20%20%7D%2C%0A%7D%3B
[19]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=let%20animal%20%3D%20%7B%20foot%20%3A%204%20%7D%3B%0Alet%20cat%20%3D%20%7B%20...animal%2C%20tail%20%3A%201%20%7D%3B
[20]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=class%20Widget%20%7B%0A%0A%20%20%20%20constructor%20(%20...args%20)%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20...%0A%20%20%20%20%7D%0A%0A%20%20%20%20method%20()%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E6%96%B9%E6%B3%95%0A%20%20%20%20%7D%0A%0A%20%20%20%20static%20foo%20()%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E7%B1%BB%E7%9A%84%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95%0A%20%20%20%20%7D%0A%7D%0A%0Aclass%20Pendant%20extends%20Widget%20%7B%0A%0A%20%20%20%20constructor%20(%20...args%20)%20%7B%0A%20%20%20%20%20%20%20%20super(...args)%3B%0A%20%20%20%20%20%20%20%20%2F%2F%20%E7%BB%A7%E6%89%BF%0A%20%20%20%20%7D%0A%0A%7D%0A%0Alet%20pendant%20%3D%20new%20Pendant()%3B
[21]: http://babeljs.cn/repl/#?experimental=true&evaluate=true&loose=false&spec=false&code=function%20readonly%20(%20target%2C%20name%2C%20descriptor%20)%7B%0A%20%20%20%20descriptor.writable%20%3D%20false%3B%0A%20%20%20%20return%20descriptor%3B%0A%7D%0A%0Aclass%20Person%20%7B%0A%20%20%20%20%40readonly%0A%20%20%20%20name%20()%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20...%0A%20%20%20%20%7D%0A%7D
[22]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=import%20%24%20from%20'jquery'%3B%0A%0Aexport%20default%20%7B%0A%20%20%20%20%2F%2F%20...%0A%7D%3B
[23]: http://babeljs.cn/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=window.jQuery%20%3D%20require('%24')%3B%0A%0Aimport%20'jquery.parallax'%3B
[24]: http://www.yy.com
[25]: http://www.yy.com
