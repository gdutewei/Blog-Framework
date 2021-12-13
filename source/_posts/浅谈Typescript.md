---
title: 浅谈Typescript
date: 2020-07-12 17:42:58
tags:
  - 前端
  - Typescript
  - Javascript
---
![](../../../../blogImg/20181004.jpg)

### 前言
&nbsp;&nbsp;&nbsp;&nbsp;Typescript在vue项目中落地实践快一年多，趁着周末闲暇时光，总结一下Typescript，本文主要介绍Typescript的发展历程及其构成（tsc，Typescript Service）、tsc编译过程、模块解析、与Bable的对比等。
<!-- more -->

### TypeScript 重要节点发展历程
1、**TypeScript 1.1发布**
&nbsp;&nbsp;&nbsp;&nbsp;这个版本重写了全部编译器代码，大幅提升性能（在白鹭引擎的实际项目测试结果至少提升了三倍），并且**不再托管在微软自身的开源代码仓库**，而是改为了在 GitHub 上托管。

2、**TypeScriptService 发布和稳定**
&nbsp;&nbsp;&nbsp;&nbsp;TypeScript 开源了其抽象语法树分析器，并提供友好的 API 接口，这被称为 TypeScriptService，这使得第三方 IDE 可以非常快速的提供 TypeScript 代码补全、类型检查、代码重构等支持，**而不是把开发者绑定在 VisualStudio 和微软体系中**。

3、**TypeScript 1.6 发布**
&nbsp;&nbsp;&nbsp;&nbsp;TypeScript 从1.5开始 开始支持 ES6 特性，并且废弃了和 ES6 矛盾的 module 关键字。从这点可以看出，在 ES6 标准出台之后，TypeScript 坚定**遵循标准**，**而非自己制定“标准”**的决心和魄力。在 1.6版本中，TypeScript 实现了几乎所有的 ES6 新特性，并能将其编译为 ES5，就像开源社区风头很劲的 Babel 一样。由于 TypeScript 遵循并实现了 ES6 标准，TypeScript 自身的价值变得更大，因为只要掌握了 TypeScript ，就相当于掌握了 JavaScript 语言的最新标准，并且能在老式浏览器上完整运行。

4、**VSCode 发布**
&nbsp;&nbsp;&nbsp;&nbsp;VSCode 是微软的一款跨平台开发工具，它**使用了大量的开源社区的优秀技术**，VSCode 包含了对一个文本编辑器来说非常优秀的 JavaScript 代码分析能力。以一个 jQuery 为例：通过一个简单的命令`npm install @types/jquery`，下载一个jQuery框架定义声明文件，可以体验这种代码分析和智能感知能力，让编辑器更懂代码，提高编程效率。
![](../../../../blogImg/2020071201.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;相信很多人会有这样的疑问：没错在VS Code里写TS很方便。但是这种不都是IDE本身提供的吗？

&nbsp;&nbsp;&nbsp;&nbsp;事实上，这些能力其实是由TS本身提供的，而这里的奥秘，就是 VSCode 采用 TypeScriptService 来分析 JavaScript 代码，以及用 TypeScript Definitions File 来做 API 支持。这意味着 TypeScript 自身已经不仅仅是一门语言，**其服务和开源社区贡献的第三方 Definitions 文件已经反哺回馈到 JavaScript 生态中**。哪怕是最固执的 JavaScript 开发者以后都可能会在不经意间用到 TypeScript 生态中的内容。

5、**Salsa项目**
&nbsp;&nbsp;&nbsp;&nbsp;Salsa 是一个 TypeScript 新版本的代号（并且确认不是2.0）。VSCode 路线图提到，通过 Salsa，JavaScript 可以被更加智能的支持。简单的理解就是，在未来，JavaScript 代码可以直接由 TypeScript 编译器编译，也就是说，在可能稍微遥远的未来，并不存在 TypeScript 这门语言，只存在经典 JavaScript （ ES5） ， ES6语法糖，类型检测混合在一起的新一代 JavaScript 语言，微软在其中只**专注做两件事**：
&nbsp;&nbsp;&nbsp;&nbsp;（1）将ES6语法翻译成ES5。
&nbsp;&nbsp;&nbsp;&nbsp;（2）在“你认为必要的地方”添加类型检查支持

### Typescript构成
1、**tsc&&类型系统**
&nbsp;&nbsp;&nbsp;&nbsp;tsc为Typescript的一个编译器，与其他编译器不同，TS的编译器不是一个黑盒，而是完全对外开放的。TS的编译器架构，包括了底层的核心Ts编译器，语言服务等，通过它你可以使用最新最稳定的JS特性，并编译成对应的ES 3 | 5 | 6 目标版本，功能类似babel。同时tsc在编译中带来了类型检查系统，使你的IDE更懂你的代码。

&nbsp;&nbsp;&nbsp;&nbsp;从Typescript源文件到执行的过程详见下表：

| 执行者 | 步骤 | 说明 | 
| ---- | ---- | ---- | 
| TSC | 1. TypeScript Source -> TypeScript AST | TSC将ts文件转为TS AST(abstract syntax tree) | 
| TSC | 2. AST is checked by typechecker | TSC的类型检查器对AST做类型检查 | 
| TSC | 3. TypeScript AST -> Javascript Source | TSC将TS AST转为JS的源代码(可能是ES3/5/6) | 
| JS(浏览器/Node.js) | 4. Javascript Source -> Javascript AST | JS运行时将JS源码转为JS AST | 
| JS(浏览器/Node.js) | 5. Javascript AST -> bytecode | JS运行时将JS AST 转为字节码，准备运行 | 
| JS(浏览器/Node.js) | 6. Bytecode is evaluated by runtime | JS运行时运行js字节码 | 

&nbsp;&nbsp;&nbsp;&nbsp;其中1-3步是TSC处理的，4-6步为JS运行时处理，可能是浏览器也可能是Node.js。

&nbsp;&nbsp;&nbsp;&nbsp;从上面步骤可以知道，TSC做类型检查是在将TS AST转为JS源码之前，也就是说从TS AST转为JS源码时，是没有做类型检查的。检查类型时针对TS AST的，即第二步。

&nbsp;&nbsp;&nbsp;&nbsp;也意味着TS的类型系统，强类型的各种机制，仅仅对类型检查有用，对产出的JS无影响，增加类型不会污染JS源文件。
![](../../../../blogImg/2020071203.jpg)

2、**Typescript Service && Language Service**
&nbsp;&nbsp;&nbsp;&nbsp;ts本身也贯彻语言及服务的理念（参考C#的Roslyn），在typescript项目中可以看到，在lib中，除了tsc之外，还有一个很重要的tsserver，通过ts server把它所支持的功能都通过TypeScript Definitions File API暴露出来。这样第三方的工具就可以通过这个api来直接使用ts语言服务的各种功能。通过这种方式，其他的IDE工具，也可以快速的集成TS的相关能力。所有的编辑器IDE都能够很方便的利用，避免重复造轮子。
![](../../../../blogImg/2020071202.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;总结一下，TypeScript 的目标是：

&nbsp;&nbsp;&nbsp;&nbsp;（1）兼容所有 JavaScript 语法，并在此基础扩展语法；
&nbsp;&nbsp;&nbsp;&nbsp;（2）静态分析代码，找出那些很有可能有 BUG 的代码；
&nbsp;&nbsp;&nbsp;&nbsp;（3）生成纯净的、可读的 JavaScript 代码，并且不会对代码作任何优化、处理，甚至连源码中的错误都保留到生成的代码中；
&nbsp;&nbsp;&nbsp;&nbsp;（4）不影响最后运行代码的环境。

&nbsp;&nbsp;&nbsp;&nbsp;静态分析代码是 TypeScript 的主要职责，通过静态分析，我们可以得到这些功能：

&nbsp;&nbsp;&nbsp;&nbsp;（1）开发中提前知道代码中的可能错误
&nbsp;&nbsp;&nbsp;&nbsp;（2）IDE 中的语法高亮、智能提示、转到定义等功能
&nbsp;&nbsp;&nbsp;&nbsp;（3）重命名变量、提取函数、自动添加导入等高级功能

### Typescript模块解析

1、概念
&nbsp;&nbsp;&nbsp;&nbsp;Typescript 模块解析就是指导 tsc 查找导入（import）内容的流程，就例如编译器通过导入语句如 `import { a } from "moduleA"` 找到 "moduleA" 模块然后找到 `a` 的定义的过程。moduleA 可能是在 `.ts` 或 `.tsx` 或 `.d.ts` 文件中。编译器首先要做的就是找到对应的模块文件。
&nbsp;&nbsp;&nbsp;&nbsp;模块导入方式有两种：相对导入和非相对导入。相对导入是以`/`，`./`或`../`开头的，内部文件(自己开发的)和外部（node_modules）中两种，其中导入内部模块称之为相对导入，导入node_modules中，称之为非相对导入，它们在语法上的区别就是导入的路径是否是相对的。

&nbsp;&nbsp;&nbsp;&nbsp;其中相对导入：
>import Entry from "./components/Entry"


&nbsp;&nbsp;&nbsp;&nbsp;非相对导入：
>import * as $ from "jQuery"

2、模块解析策略

&nbsp;&nbsp;&nbsp;&nbsp;两种可用的模块解析策略：`Node`和`Classic`。 你可以使用 --moduleResolution标记来指定使用哪种模块解析策略。若未指定，那么在使用了 --module AMD | System | ES2015时的默认值为Classic，其它情况时则为Node。

&nbsp;&nbsp;&nbsp;&nbsp;（1）Classic 策略：这种策略在以前是TypeScript默认的解析策略。 现在，它存在的理由主要是为了向后兼容。

&nbsp;&nbsp;&nbsp;&nbsp;**Classic 策略相对导入的模块是相对于导入它的文件进行解析。**

&nbsp;&nbsp;&nbsp;&nbsp;例如：
>// 路径： /root/src/folder/A.ts
>import { b } from "./moduleB"


&nbsp;&nbsp;&nbsp;&nbsp;查找流程如下：
>1. /root/src/folder/moduleB.ts
>2. /root/src/folder/moduleB.d.ts

&nbsp;&nbsp;&nbsp;&nbsp;**Classic 策略非相对模块的导入，编译器则会从包含导入文件的目录开始依次向上级目录遍历，尝试定位匹配的声明文件。**

&nbsp;&nbsp;&nbsp;&nbsp;例如：
>//路径： /root/src/folder/A.ts
>import { b } from "moduleB"

&nbsp;&nbsp;&nbsp;&nbsp;查找流程如下：
>1. /root/src/folder/moduleB.ts
>2. /root/src/folder/moduleB.d.ts
>3. /root/src/moduleB.ts
>4. /root/src/moduleB.d.ts
>5. /root/moduleB.ts
>6. /root/moduleB.d.ts
>7. /moduleB.ts
>8. /moduleB.d.ts

&nbsp;&nbsp;&nbsp;&nbsp;(2) Node 解析策略：这个解析策略试图在运行时模仿Node.js模块解析机制。 完整的Node.js解析算法可以在 [Node.js module documentation](https://nodejs.org/api/modules.html#modules_all_together)找到。

&nbsp;&nbsp;&nbsp;&nbsp;**Node策略相对模块解析**
&nbsp;&nbsp;&nbsp;&nbsp;例如：
>// 文件/root/src/moduleA.ts
>import { b } from "./moduleB"

&nbsp;&nbsp;&nbsp;&nbsp;查找流程如下：
>1. /root/src/moduleB.ts
>2. /root/src/moduleB.d.ts
>3. /root/src/moduleB/package.json (如果指定了"types"属性)
>4. /root/src/moduleB/index.ts
>5. /root/src/moduleB/index.d.ts

&nbsp;&nbsp;&nbsp;&nbsp;**Node策略非相对模块导入**
&nbsp;&nbsp;&nbsp;&nbsp;例如：
>// 文件/root/src/moduleA.ts
>import { b } from "moduleB"

&nbsp;&nbsp;&nbsp;&nbsp;查找流程如下：
>1. /root/src/node_modules/moduleB.ts
>2. /root/src/node_modules/moduleB.d.ts
>3. /root/src/node_modules/moduleB/package.json (如果指定了"types"属性)
>4. /root/src/node_modules/moduleB/index.ts
>5. /root/src/node_modules/moduleB/index.d.ts
>6. /root/src/node_modules/@types/moduleB

### Typescript VS Babel
&nbsp;&nbsp;&nbsp;&nbsp;1、Babel是一个免费的开源JavaScript编译器。转置器(源代码到源代码编译器)是一种工具，它读取用一种编程语言编写的源代码，然后用另一种编程语言生成相同的代码。Babel主要用于将ES6 (ECMAScript 2015)或以上版本代码转换为JavaScript的向后兼容版本(ES5)，可以在任何浏览器中运行。它是使用JavaScript编程语言最新特性的流行工具。
&nbsp;&nbsp;&nbsp;&nbsp;2、TypeScript是一种开源的纯面向对象的编程语言，它是一个强类型的JavaScript超集，通过tsc可以编译成纯JavaScript。我们不能直接在浏览器上运行TypeScript程序。它需要tsc来编译和生成JavaScript文件，直接在浏览器上运行。
![](../../../../blogImg/2020071204.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;从下表中我们可以了解Typescript和Babel之间的主要区别

| 编号 | Typescript | Babel | 
| ---- | ---- | ---- | 
| 1 | TypeScript是一种开源的纯面向对象的编程语言。它是一个强类型的JavaScript超集，可以编译成纯JavaScript。 | Babel是一个免费的开源JavaScript编译器。它主要用于将ES6 (ECMAScript 2015)或以上版本代码转换为可在任何浏览器上运行的向后兼容的JavaScript版本(ES5)。 | 
| 2 | 它是一种编程语言。 | 它是一个工具(转译器)。 | 
| 3 | TypeScript提供数据类型的类型检查。 | Babel不关心类型。 | 
| 4 | TypeScript一次编译整个项目。 | Babel一次只能编译一个文件。 | 
| 5 | Typescript使开发人员能够使用优秀的输入功能。它适用于大型应用程序。 | Babel适合希望使用最新语言特性编写纯JavaScript代码的开发人员。| 
| 6 | TypeScript是JS的附加组件，支持强类型。 | Babel是一个转置器(工具)，它将较新的JS语法特性作为输入，并返回较旧/更可靠的语法作为输出。 | 
| 7 | 它是由微软开发和维护的。 | 它与ECMA技术委员会39 (TC39)密切相关。 | 
| 8 | TypeScript直接编译装饰器。 | Babel不直接编译装饰器。它有一个旧版本的遗留模式来编译装饰器。 | 

&nbsp;&nbsp;&nbsp;&nbsp;Babel也是很不错的ES6 to 5编译工具，有不错的插件机制，社区发展也不错，但在同样一段代码编译出的JS代码里可以看到，TS编译后的代码是更符合习惯、简洁易读一些。
![](../../../../blogImg/2020071205.jpg)

![](../../../../blogImg/2020071206.jpg)

### Typescript编译最佳实践方案 - Babel支持编译Typescript
&nbsp;&nbsp;&nbsp;&nbsp;目前 TypeScript 的编译有两种方式。一种是使用 TypeScript 自家的编译器 tsc 编译，一种就是使用 Babel + @babel/preset-typescript 编译。所以，当我们使用 TypeScript 开发项目的时候，遇到的第一个问题就是，我们应该选择哪种编译方式？

&nbsp;&nbsp;&nbsp;&nbsp;**Babe 编译的优势**
&nbsp;&nbsp;&nbsp;&nbsp;（1）灵活性：**Babel 能够根据目标环境转译指定语法。这一点 tsc 是不支持的**。tsc 只能指定将 TypeScript 编译为 es3 es5 es6 或类似的某个 ECMAScript 版本。但是在 Babel 里通过 @babel/preset-env你可以指定目标环境，比如 "targets": { "ie": "11" }，那么 Babel 只会编译 ie11 不支持的语法，所有 ie11 支持的语法 Babel 都不会做转译。在编译的灵活性上，只要你想，你可以控制 Babel 只编译你需要编译的语法。
&nbsp;&nbsp;&nbsp;&nbsp;（2）polyfill：**Babel 能够根据目标环境自动添加 polyfill。这一点 tsc 是不支持的**。如果是新语法的转译，tsc 会添加一些辅助函数。但是任何需要修改运行时环境的 polyfill，tsc 是不会帮你添加的。比如你的代码中用到了 PromiseSetMap或者 Object.assignArray.includes，那么你需要自己手动添加相应的 polyfill。但是在 Babel 里通过@babel/preset-env，Babel 会判断目标环境，然后自动帮你添加所有你需要用到的 polyfill。
&nbsp;&nbsp;&nbsp;&nbsp;（3）插件系统：**Babel 有插件机制，并且有着活跃的插件生态**。这一点 tsc 是不支持的。tsc 没有插件系统，并不允许你添加自己的插件。但是在目前的开发中，我们都或多多少的受益于 Babel 各种各样的插件，而且很多人也都写过自己的 Babel 插件，去自定义转译规则。

&nbsp;&nbsp;&nbsp;&nbsp;总结：**Babel 支持编译 TypeScript 才是最好的选择**。
![](../../../../blogImg/2020071207.jpg)
&nbsp;&nbsp;&nbsp;&nbsp;TS 编译和 Babel 编译的优缺点如上。无论如何，tsc 都是必须的。即使使用 Babel 编译，也应该配合 tsc 一起使用，利用 tsc 做类型检查，然后使用 Babel 完成转译工作。至于你是否应该使用 Babel 编译，要看你是否需要 Babel 编译的优势，是否依赖 Babel 生态下的各种插件。
&nbsp;&nbsp;&nbsp;&nbsp;总的来说，tsc的功能没有babel多，扩展性也没有babel强，但是对于tsc所覆盖的那一部分（也就是ts），tsc做得比babel更好更精，而ts，很多时候也就恰恰是Javascript工程实践中所需要的那一部分。

### 参考资料
1.[Zhihu - 现在Typescript的生态如何](https://www.zhihu.com/question/37222407)
2.[TypeScript 源码详细解读](https://www.cnblogs.com/xuld/p/12180913.html)
3.[模块解析 - Typescript中文网](https://www.tslang.cn/docs/handbook/module-resolution.html)
4.[为什么 Babel 要支持编译 TypeScript](https://www.javascriptcn.com/read-87256.html)