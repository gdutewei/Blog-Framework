---
title: Typescript体系调研
date: 2020-07-05 15:35:29
tags:
  - 前端开发
  - ES6
  - Typescript
---
![](../../../../blogImg/20181006.jpg)

### Typescript起源

&nbsp;&nbsp;&nbsp;&nbsp;说到TypeScript，就不得不提Javascript，Javascript作为一门非常有争议的语言，发展到今天成为当下最流行的语言的过程是非常戏剧性的。有很多必然，也有很多偶然。前端社区有关js的争论，也一天没有消停过。
<!--more-->

&nbsp;&nbsp;&nbsp;&nbsp;1995 年，受雇于 Netscape 的 Brendan Eich 用了十天时间设计出了 JavaScript。之后便开启了浏览器兼容和争夺的至暗时刻，到 1997 年 ECMA 组织开始发布公开标准，JavaScript 即将进入标准化进程。得益于 ECMA 的标准，JavaScript 愈发的强大，并借助 Babel 实现了标准制定和浏览器实现的兼容，使得我们可以写最现代化的代码而不用过多的考虑浏览器兼容性，并且还诞生 Node.js、React Native 等服务器端、移动端的 JavaScript 运作方式，谁也想不到二十年后的今天 JavaScript 似乎印证了 Write Once Run Anywhere 的优势。

&nbsp;&nbsp;&nbsp;&nbsp;在过去，很多人把Javascript当做是一个玩具语言。我们也会发现在某些场景，使用Javascript的人员并不一定是开发者（譬如早期qq空间通过脚本装饰页面）。更可以毫不夸张的说，很多开发者觉得，Javascript是一门，等真正需要用到的时候，再去随意学学，就能上手的语言。种种原因导致了Javascript在很多时候被滥用。

&nbsp;&nbsp;&nbsp;&nbsp;当然Javascript本身的确是存在非常多的问题，尤其在早期的时候。没有`模块`、`class`、`类型`。还有一堆为人所诟病的语言设计，`null`、`undefined`、`NaN`等等。

&nbsp;&nbsp;&nbsp;&nbsp;虽然JS有诸多糟粕，但是在浏览器里，你没办法摆脱他。开发者们想出了“用我喜欢的语言来编译生成JS”这样的点子，把JS仅仅当作媒介语言。慢慢的，开发者觉得这种方式有点不伦不类，不如彻底一点，干脆发明一些新的语言来取代JS。这里面最为出名的就是微软的`Typescript`，Google的`Dart`与`CoffeeScript`。

&nbsp;&nbsp;&nbsp;&nbsp;TypeScript 起源于使用JavaScript开发的大型项目 。由于JavaScript语言本身的局限性，难以胜任和维护大型项目开发。因此微软开发了TypeScript ，使得其能够胜任开发大型项目。在 2012 年 10 月，微软发布了首个公开版本的TypeScript，2013年6月19日，在经历了一个预览版之后微软正式发布了正式版TypeScript，当前最新版本为TypeScript 4.0。

### 如何定义Typescript

&nbsp;&nbsp;&nbsp;&nbsp;1、TS官网下的定义为“`JavaScript that scales`”，Scales意味着“规模扩大”。而对应的中文官网直接翻译成“`JavaScript的超集`"，显然是有点文不对题的。然而，这却恰好从两个不同的层面解释了什么是TypeScript。

&nbsp;&nbsp;&nbsp;&nbsp;英文版明确了TS与JS的能力区分: **TS更能适应项目规模不断扩大的场景**。

&nbsp;&nbsp;&nbsp;&nbsp;中文版则解释了TS的本质是什么： **它是一种具有类型系统的JS的超集**。

&nbsp;&nbsp;&nbsp;&nbsp;2、TS不仅仅是一门语言，也是一种生产力工具，因为TS包含一个`编译器`，通过它你可以使用最新最稳定的JS特性，并编译成对应的ES目标版本，功能类似babel。此外最核心的部分是TS带来类型系统，通过TS Server可以使你的IDE可以更容易的理解你的代码，增强了IDE在 **智能提示**，**跳转定义**，**代码补全** 等方面的功能，并且在tsc编译阶段能发现大部分的类型错误，来帮助你更高效的写高质量的代码，对于大型工程的代码可读性和可维护性起到了至关重要的作用。

&nbsp;&nbsp;&nbsp;&nbsp;所以总结起来 **TS不仅仅是一门语言，也是生产力工具**。

### ECMAScript、Javascript、ES6及Typescript

&nbsp;&nbsp;&nbsp;&nbsp;1.ECMAScript 是Ecma组织(国际计算机制造商协会)制定的标准化脚本语言，JavaScript语言是参考这个标准来实现的。

&nbsp;&nbsp;&nbsp;&nbsp;2.ECMAScript6增添了许多特性，例如：模块和类，Maps、Sets、Promises、生成器（Generators）等，使得JavaScript语言可以用来编写大型的复杂的应用程序，但是主流的宿主环境（无论是浏览器环境还是服务器环境）不能完全支持ES6，导致了开发者真正要使用ECMAScript6时，需要将ECMAScript6代码进行转译。

&nbsp;&nbsp;&nbsp;&nbsp;3.TypeScript 是一种微软开源的编程语言，因为JavaScript是弱类型语言，所以TypeScript为JavaScript扩展类和模块的概念，并添加了类型系统，所以本质上 Typescript = Type + JavaScript。TypeScript支持ECMAScript6标准（实际上相当于是对ECMAScript6的提前实现），并且能将代码根据需求转换为 ES 3 / 5 / 6。这意味着开发者可以通过TypeScript使用最新的ECMAScript特性，无需再考虑兼容性的问题。

&nbsp;&nbsp;&nbsp;&nbsp;Typescript相对于ES5有五大改善：
&nbsp;&nbsp;&nbsp;&nbsp;（1）类型
&nbsp;&nbsp;&nbsp;&nbsp;（2）类
&nbsp;&nbsp;&nbsp;&nbsp;（3）注解
&nbsp;&nbsp;&nbsp;&nbsp;（4）模块导入
&nbsp;&nbsp;&nbsp;&nbsp;（5）语言工具包（比如结构）
![](../../../../blogImg/2020070503.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;和TypeScript 相似的工具语言还有很多，主要分为两个阵营：
&nbsp;&nbsp;&nbsp;&nbsp;（1）一个是类似 `Babel` 的阵营，坚持JavaScript 的语法风格编写，为开发者提供最新的 ECMAScript 特性；
&nbsp;&nbsp;&nbsp;&nbsp;（2）另一个则是`Coffeescript`、`Clojure`、`Dart`等的阵营，它们的语法与 JavaScript 迥然不同，但最终会编译为JavaScript；

### Dart、CoffeScript和TypeScript对比和思考

&nbsp;&nbsp;&nbsp;&nbsp;在百度指数中，把CoffeeScript、Dart、TypeScript一起搜索。可以看到，从2013年至今，CoffeeScript基本保持在比较低的水平，Dart由于flutter的影响从2018年开始攀升，而TS却一直在攀升并保持在一个较高的水平。
![](../../../../blogImg/2020070501.jpg)

* CoffeeScript从2009年出现到现在，已十分成熟。从语法上看，CoffeeScript更像Ruby，写起来比较随意，而TypeScript更接近于C#。然而TypeScript正在超越CoffeeScript，成为大家的首选。

* TypeScript是通过类似于垫片(Shim)的技术进行代码转化，生成与现有js完全兼容的代码，从本质上讲它就是JavaScript。另外，由于TypeScript 是微软的产品，所以在Visual Studio工具上有良好的支持。

* Dart最初是由 Google 的 Chrome V8 团队打造。与TypeScript编译JavaScript代码不同，Dart是跳过翻译的步骤，直接在浏览器里面嵌入一个 Dart 解释引擎与 V8 并行。相比起TS和CS，使用Dart的人相对较少。

&nbsp;&nbsp;&nbsp;&nbsp;为什么TS可以，而其他这些语言却没法成为主流呢？这其中主要有三个原因：

&nbsp;&nbsp;&nbsp;&nbsp;1.没有严格遵从ECMAScript的规范。语法层面他们和JS是完全割裂的。譬如CoffeeScript用的是接近于ruby的语法，当使用这样的语言的时候，你会感觉你是完全在学一门新语言。有一定的学习成本。在ECMAScript规范不断演进的情形下，这类语言的语法就会越来越成为累赘。

&nbsp;&nbsp;&nbsp;&nbsp;2.性能问题。这在早期的时候更为明显，比如Dart语言，在用Dart的编译器转化为JS后，编译耗时过长，不做任何优化的情况下，会产生了n多行代码。这显然是难以接受的。

&nbsp;&nbsp;&nbsp;&nbsp;3.生成代码的可读性差，没有办法回退。毕竟只是把JS做为媒介语言，JS的可读性不是这类语言的考量。这也意味着一旦项目启动，就没法很轻松的回退回原生JS。

### Typescript与JavaScript的对比表格

| 对比项目 | TypeScript | JavaScript | 注意 | 
| --------| --- | --- | --- | 
| 基本类型 |  boolean number string Array Tuple Enum any void null undefined never object | string number boolean null undefined symbol | TypeScript 中 object 表示的是不是 JavaScript 基本类型的类型| 
| 变量声明 | let const var| let const var | 基本一致 | 
| 接口 | interface | 无 |  TypeScript 的核心是类型检查，因此接口充当了命名这些类型的角色 | 
| 类 | class abstract class  readonly … | class 无 abstract class | 基本一致，但不同的可能发生在未来，TypeScript 使用 private 来定义私有，而 JavaScript 未来极有可能将 #.xx 来定义私有写入标准。TypeScript  支持抽象类，只读等等。| 
| 函数 | N | N | 基本一致，参数赋默认值，剩余参数等等，唯一不同的是 TypeScript 支持?可选参数 | 
| 泛型 | Generics | 无 | 泛型是一个特别灵活的可重用指定不同类型来控制具体类型的类型，TypeScript 支持 | 
| 枚举 | Enums | 无 | TypeScript 支持的枚举不仅可以默认从 0 开始，也可以赋值具体的字符串，它的操作空间非常大 | 
| 类型推断 | 支持 | 无 |  let x = 3; TypeScript 可以通过 3 来推断 x 的类型是 number | 
| 高阶类型 | & typeof  instanceof … | 无 | TypeScript 独有 | 
| Symbols | N | N | Symbol 一样 | 
| 迭代器 | N | N | 如果实现了 Symbol.iterator ，那么就被视为可迭代的，术语上和 JavaScript 定义的一样 | 
| Generators | N | N | 一样 |
| 模块系统 | N | export import | 事实上 TypeScript 支持多种多样的模块系统，既有 ESModule 也有 Commonjs 规范，甚至还有 AMD UMD 等 |
| 其他 | N | N | 由于 TypeScript 是 JavaScript 的超集，因此 ES2016 之后以及 ESNext 定义的  api 都可以直接在 TypeScript 中使用 并不需要语言支持，至于其他一些比如 JSX Mixins 等等，由于这些不属于 JavaScript 标准因此这里不再复述 。|

### TypeScript 的流行趋势

&nbsp;&nbsp;&nbsp;&nbsp;事实上 TypeScript 拥有活跃的社区，大部分第三方库都有提供 TypeScript类型定义文件，甚至知名的前端或后端库都完全使用 TypeScript 来进行开发，比如 Google 的 Angular，Nest.js, 还有一些著名的 UI 组件库，如蚂蚁金服的 Ant Design，Google 的 Material Design，我们在平时工作中实实在在使用的库或框架（vue、react等）都使用了  TypeScript 构建或正在调研使用中...

&nbsp;&nbsp;&nbsp;&nbsp;我们可以通过一些数据来了解 TypeScript 的流行趋势：
&nbsp;&nbsp;&nbsp;&nbsp;1、在百度指数中，把JavaScript、ES6、TypeScript一起搜索，可以看到Typescript一直处于攀升阶段
![](../../../../blogImg/2020070502.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;2、StackOverFlow的报告，在程序员最喜欢的语言中，TS与Python目前并列第二，仅次于Rust。
![](../../../../blogImg/2020070504.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;3、Npm包的开发者中，高达62%的开发者在使用TS。
![](../../../../blogImg/2020070505.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;从这些数字中可以很明显的看出，当下TS已经取得了相当惊人的成就。

### TS会取得如此成功主要有5个原因

&nbsp;&nbsp;&nbsp;&nbsp;1.对类型安全的诉求。无论在浏览器还是服务端，前端项目规模越来越大，越来越复杂。而规模越大，对静态类型语言的诉求就越强烈。

&nbsp;&nbsp;&nbsp;&nbsp;2.严格遵守ECMAScript规范。与那些把JS当作媒介语言的语言是不同的。TS选择改进了JS，而不是取代它。

&nbsp;&nbsp;&nbsp;&nbsp;3.采用Structural Typing而不是Nominal Typing。面向对象的语言，一般使用nominal typing(C++, Java, Swift)，而函数式语言更习惯使用Structural Typing（OCaml, Haskell, Elm）。JS里面，你即可以使用面向对象，又可以使用函数式。但js的开发者通常更倾向于使用函数式编程。这种情况下，TS选择了使用结构类型，也更符合js开发者的编程习惯。

&nbsp;&nbsp;&nbsp;&nbsp;4.强大的开发工具。正如我前面提到的，通过工具提高生产力才是TS的核心目标。TS本身提供了非常棒的工具支持，它的TS Server机制是非常有创造性的。

&nbsp;&nbsp;&nbsp;&nbsp;5.Open Source， Open Development。TS是以100%的开放开发的方式来运营的。也就是说有关与ts的一切，都是对开发者100%透明的。在过去，当你给一门语言提一个bug的之后，可能等一两年才会出新版本，而到那个时候你才会发现，你提的bug可能根本没被修复。通过TS的roadmap你可以清晰的看到具体哪些bug会被修复，哪些feature会被新增，以及所有关于这些技术点的讨论。这样拉近了核心开发团队与使用者的距离，让TS的社区非常的活跃。

### TypeScript 的优势和收益及劣势是什么？

&nbsp;&nbsp;&nbsp;&nbsp;1、优势与收益
* 更少的bug，伦敦大学与微软研究院的一些学者，发表了一篇相当有影响力的论文。文中指出，15%的github公开bug，是可以通过Typescript来规避的，类型系统可在编译阶段发现大部分的错误
* 类型系统也是一个很直观的编程文档，可以查看任何函数或API的输入输出类型，方便阅读、增强了编辑器或IDE的功能，自动的推导类型，提高生产力（TS Server）
* 一切 JavaScript 都是合法的 TypeScript 降低了使用成本
* TypeScript 拥抱 ES2015 以及 ESNext 草案规范
* 强大的社区支持，几乎第三方库都有 TypeScript 类型定义文件（DenitelyTyped）
* 框架反哺，众所周知，一些非常有影响力的前端框架的新版本都开始用ts来进行重写了，Angular 2， Vue3等等。而这些社区中的开发者，都是开源社区最活跃的参与者，他们会将开发过程中遇到的ts的一些问题，通过PR或者反馈的方式再反哺到ts社区中，让ts的生态越来越好。

&nbsp;&nbsp;&nbsp;&nbsp;2、劣势
* 学习成本
* 开发效率的降低
* 部分三方库的兼容
* 需要编译

&nbsp;&nbsp;&nbsp;&nbsp;当然，凡事都有两面性，TypeScript 有一定的学习成本，比如：Interfaces，Generics，Enums 等前端工程师不是很熟悉的概念，短期内多少会增加一些开发成本，集成和构建一些库会有一定的工作量。

### 我们对于TypeScript的使用

&nbsp;&nbsp;&nbsp;&nbsp;1、对新技术的尝试。组内人员对新技术的热忱度都很高，希望通过一个项目来实践TypeScript。
&nbsp;&nbsp;&nbsp;&nbsp;2、多人协作，项目庞大且持续维护，依靠Typescript强大的类型系统，每个人编写时都可以避免低级的类型错误引发的bug，TypeScript的使用可以方便大家阅读和后续扩展、重构。
&nbsp;&nbsp;&nbsp;&nbsp;3、代码规范化，新项目。从头开发，没有重构老代码的成本。

&nbsp;&nbsp;&nbsp;&nbsp;总结：是否使用TypeScript，在做出选择之前，需要认真的衡量一下投入产出比，TypeScript带来的优势是否对当前的项目有很大提升，是否值得花费大量的时间去对现有项目进行重构，值得注意的一点是，不管TypeScript最终会不会被应用到项目中，你都应该学会掌握它了，不要人云亦云。最后，对于项目Typescript取舍问题，如果项目是大型项目，第三方库，或者其他需要持续维护的项目，上TypeScript吧；如果项目是活动，分享页面，等短周期并且不需要持续维护的项目，想用哪个用哪个，主要看个人追求。

&nbsp;&nbsp;&nbsp;&nbsp;有很多人会问，TypeScript会不会像CoffeeScript、ActionScript一样，在JavaScript引入标准后逐渐被抛弃，那我们还有学习的必要么？不排除有这样的可能性，但是我们没办法确定这个等待期有多长，即便是后续会被JavaScript引入标准，在这之前你就可以享受到上面我们所说的便利，这不香么？也许若干年后，JavaScript也不复存在了呢，哈哈。


### 参考资料
1.TypeScript 百度百科：https://baike.baidu.com/item/typescript/4314718

2.未来可期的TypeScript：https://www.infoq.cn/article/UJi4x9fUcaw9fCJ52o8i

3.万物起源-从 JavaScript 到 TypeScript：https://zhuanlan.zhihu.com/p/61345416

4.解惑ECMAScript/JavaScript/TypeScript和CoffeeScript等概念：https://www.jianshu.com/p/9bc987ebb85c



