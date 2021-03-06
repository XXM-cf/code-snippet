JS基础考题：
- 变量的类型和计算
- 原型和原型链
- 作用域和闭包

----

原型和原型链: 
- Object是超级对象，原型链的顶端到Object.prototype，其中Object.prototype.__proto__为null。
- 所有引用类型都有一个隐式原型对象：__proto__
- 普通函数都有一个prototype对象，他是一个普通对象

```js
function fn () {}
console.log(fn.__proto__ === Function.prototype)
console.log(Function.prototype.__proto__ === Object.prototype)
console.log(Object.prototype.__proto__ === null)
```

instanceof:
- fn instanceof Foo查找逻辑
  - 看fn的__Proto__一层层往上，能否对应到Foo.prototype

原型链继承：
子类的原型对象实例化父类。

---- 

作用域和闭包:

- 变量提升的理解
- this的几种使用场景
- 10个a标签，点击弹出对应序号
- 如何理解作用域
- 实际开发中闭包的应用

执行上下文：
- 一段script标签或一个函数：生成一个执行上下文

this:
- this要在执行时才能确认值，定义时无法确认。
- 使用场景
  - 作为构造函数中执行
  - 作为对象属性执行
  - 作为普通函数执行
  - call bind apply

当前作用域没有定义的变量称为自由变量。

闭包的使用场景：
- 函数作为函数返回值
- 函数作为函数参数 

-----

异步和单线程
- 同步异步区别，分别举一个例子（定时器，alert）
- setTimeout笔试题
- 前端使用异步的场景（可能发生等待的情况：定时器，ajax请求，事件绑定）

---- 

日期：

Math：

数组API：

对象API：

------

开发环境：加快开发效率
- IDE（写代码的效率）
- Git（代码版本管理，多人协作开发）
- JS模块化
- 打包工具
- 上线回滚的流程

----

IDE：
- webstorm：收费
- sublime：轻量级，打开快
- vscode：微软轻量版VS
- atom：github开源的编辑器

后面三个编辑器，本身功能不多，需要依赖插件进行编码。

----

Git：
- 正式项目都需要代码版本管理、版本回退等
- 大型项目多人协作，解决代码合并问题
- git linux同一个作者

免费的git服务：coding.net github.com

一般公司都有自己的git服务器（搭建工作无需了解太多）

git基本命令和操作.....

------

模块化：
假如有三个JS文件，until.js  a-until.js a.js，a.js依赖a-until.js中的函数，a-until.js依赖until.js里的函数

不使用模块化情况：
- 每个JS文件依次引入，并且until.js  a-until.js中外界需要用到的函数都暴露到全局，污染全局变量
- 依赖关系不明显（负责编写a.js文件的人，并不一定知道需要用到until.js文件）

使用模块化情况：
- 页面只需引a.js，其他的根据依赖关系自动引入
- until.js  a-until.js中暴露的函数无需做成全局

AMD:require.js
- 全局define函数
- 全局require函数
- 依赖JS会自动、异步加载

CommonJs(服务器端，硬盘同步读取):

- nodejs模块化规范，前端开发的依赖（插件和库）都可以npm下载（package.json）
- 构建工具高度自动化（自动编译、压缩、打包）
- 同步一次性加载

对比：
- 异步加载JS，用AMD
- 用npm用CommonJS

----

构建工具：
- grunt
- gulp
- fis3
- webpack(目前常用)

----
上线回滚：
- 基本流程
- linux基本命令（买个服务器练练）

基本流程：
上线
- 将测试完成的代码提交master分支
- 将当前服务器的代码全部打包并记录版本号，备份
- master分支代码提交覆盖到线上服务器，生成新的版本号

回滚
- 将当前服务器的代码全部打包并记录版本号，备份
- 将备份的上一个版本解压，覆盖到线上服务器，并生成新的版本号

linux基本命令：

```bash
# login
ssh name@server # 回车会让你输入用户名、密码

# 创建目录
mkdir content
ls
ll
cd content 
pwd
cd ..
rm -rf content
cp a.js a1.js
mv a1.js src/a1.js
rm a.js

# vi编辑器
vi a.js
i
esc
esc:w 
esc:q
wsc:wq

# 查看文件内容
cat a.js

# 查看前一些
head a.js
head -n 1 a.js
# 查看后面一些
tail a.js
tail -n 2 a.js

# 搜索操作
grep '2' a.js

```

------

运行环境：（浏览器）
- 浏览器通过访问链接来得到页面内容
- 通过绘制和渲染，显示出页面最终样子
- 整个过程中需考虑的问题
  - 页面加载过程
  - 性能优化
  - 安全性

------

页面加载：

- 输入URL到得到html的详细过程
- window.onload（页面全部资源加载完才执行，包括媒体资源）和DOMContentLoaded（DOM渲染完即可执行）区别

加载资源的形式、加载一个资源的过程、浏览器渲染页面的过程

加载资源的形式：
- 输入URL或跳转 加载HTML
- 加载html中的静态资源

加载一个资源的过程：
- 浏览器根据DNS服务器得到域名的IP地址
- 向这个IP的机器发送http请求
- 服务器收到、处理并返回http请求
- 浏览器得到返回内容

浏览器渲染页面过程：
- 根据HTML结构生成生成DOM树
- 根据CSS生成CSSOM
- 将DOM和CSSOM整合形成RenderTree（渲染树）
- 根据 RenderTree 开始渲染和展示
- 遇到script标签时，会执行并阻塞渲染（JS可能更改DOM树，所以等待JS加载执行）

思考：
- CSS放到head中（如果不，出现跳动卡东、性能太差、渲染了两次）
- JS放到body下面（防止页面渲染阻塞）
- 图片是异步加载

----

性能优化：
- 多使用内存、缓存或者其他方法
- 减少CPU计算、减少网络

从这里入手：
- 加载页面和静态资源
- 页面渲染

加载资源优化：
- 静态资源合并压缩
- 静态资源缓存（浏览器策略）
- 使用CDN让资源加载更快
- 使用SSR后端渲染，数据直接输出到HTML中

渲染优化：
- CSS放前面，JS放后面
- 懒加载（图片懒加载，下拉加载更多）
- 减少DOM查询，对DOM查询做缓存
- 减少DOM操作，多个操作尽量合并在一起执行
- 事件节流(多次同一个事件操作，可以设置个定时器（每次判断是否有这个定时器，若有则清除定时器），直到最后一次操作，则会执行一次定时器的逻辑)
- 尽早执行操作（如DOMContentLoaded）

-----
安全性：
大多是后端做的（数据库，服务器层面的）
- XSS跨站请求攻击
- XSRF跨站请求伪造

XSS：
- 写博客插入一段script标签
- 攻击代码中，获取cookie，发送自己的服务器

预防：
- 替换： <为&lt 等
- 后端替换

XSRF:
- 登录购物网站，正在浏览商品
- 付费接口是xxxxx.com/pay?id=100，但没有任何验证
- 收到一封邮件，隐藏着一个图片，地址就是付费接口

预防：
- 增加验证流程（输入指纹、密码、短信验证码）
- 后端验证

------
面试技巧：
- 简历
- 过程

简历：
- 简洁明了，重点突出项目经历和解决方案（项目简介、用了什么技术、难点，怎么解决）
- 个人博客放在简历中，定期维护更新博客
- 开源项目放在简历中，并维护
- 简历别造假（能力经历真实性）

过程：
- 如何看待加班（加班就像借钱，救急不救穷）
- 不可挑战面试官，不要反考面试官
- 学会给面试官惊喜，但不要太多
- 遇到不会回答的问题，说出你知道的也可以
- 谈谈你的缺点（说说你最近正在学什么就可以了）
