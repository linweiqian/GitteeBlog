---
title: 深入了解前端开发规范的区别《Commonjs、AMD、CMD、ES6模块化》
tags: 
- 前端面试
- 八股文
categories:
- 八股文
---
## commonjs规范 （Node.js）:
CommonJS 主要运行于服务器端，该规范指出，一个单独的文件就是一个模块，其内部定义的变量是属于这个模块的，不会对外暴露，也就是说不会污染全局变量。 Node.js为主要实践者，它有四个重要的环境变量为模块化的实现提供支持：module、exports、require、global。

> CommonJS的核心思想就是通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 或者
> module.exports 来导出需要暴露的接口

- 优点：CommonJS规范在服务器端率先完成了JavaScript的模块化，解决了依赖、全局变量污染的问题，这也是js运行在服务器端的必要条件。

- 缺点：由于 CommonJS 是同步加载模块的，在服务器端，文件都是保存在硬盘上，所以同步加载没有问题，但是对于浏览器端，需要将文件从服务器端请求过来，那么同步加载就不适用了，所以，CommonJS是不适用于浏览器端的。
<!--more-->
## AMD 规范（require.js）：
AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"。它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

> 模块功能主要的几个命令：define、require、return和define.amd。define是全局函数，用来定义模块,define(id?, dependencies?,factory)。require命令用于输入其他模块提供的功能，return命令用于规范模块的对外接口，define.amd属性是一个对象，此属性的存在来表明函数遵循AMD规范。

- 优点：适合在浏览器环境中异步加载模块。可以并行加载多个模块。
- 缺点：提高了开发成本，并且不能按需加载，而是必须提前加载所有的依赖。
## CMD 规范（sea.js）:

> CMD通过按需加载的方式，而不是必须在模块开始就加载所有的依赖。 CMD推崇依赖就近、延迟执行。

- 优点：同样实现了浏览器端的模块化加载。可以按需加载，依赖就近。
- 缺点：依赖SPM打包，模块的加载逻辑偏重。
## ES6模块化：

> ES modules（ESM）是 JavaScript 官方的标准化模块系统。

在ES6中，我们可以使用 import 关键字引入模块，通过 export 关键字导出模块，但是由于ES6目前无法在浏览器中执行，所以，我们只能通过babel将不被支持的import编译为当前受到广泛支持的 require。

## 总结：
- AMD/CMD/CommonJs 是js模块化开发的规范，对应的实现是require.js/sea.js/Node.js
- CommonJs 主要针对服务端，AMD/CMD/ES Module主要针对浏览器端(服务端一般采用同步加载的方式，浏览器端需要异步加载)
- AMD/CMD区别，虽然都是并行加载js文件，但还是有所区别，AMD是预加载，在并行加载js文件同时，还会解析执行该模块（因为还需要执行，所以在加载某个模块前，这个模块的依赖模块需要先加载完成）；而CMD是懒加载，虽然会一开始就并行加载js文件，但是不会执行，而是在需要的时候才执行。
- CommonJs和ES Module的区别：
-- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
-- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
-- CommonJS 模块的require()是同步加载模块，ES6 模块的import命令是异步加载，有一个独立的模块依赖的解析阶段。
