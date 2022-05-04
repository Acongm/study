# 现代包管理器 - npm/yarn/pnpm 的选择

##  javascript 包管理的历史
- npm 出现之前：前端依赖项是保存到存储库中并手动下载的📁
- 2010：npm 发布并支持 nodejs📦
- 2012：npm 的使用量急剧增加——主要是由于 Browserifys 浏览器的支持🎉
- 2012：npm 有了一个竞争对手 bower，它完全支持浏览器💻
- 2012-2016：前端项目的依赖项数量成倍增加🤯
- 2012-2016：构建和安装前端应用变得越来越慢🐢
- 2012-2016：大量（重复的）依赖项存储在神奇的 node_modules 内的嵌套文件夹中☢️
- 2012-2016：rm -rf node_modules 成为前端开发人员最常用的命令。 🗑
- 2015：bower 输给了 npm  💀
- 2015：node_modules 被修改为扁平化的文件结构！ 🕸
- 2016： left-pad成为当时的新闻头条 👈
- 2016： yarn 发布 🚀
  - 支持 npm 和 bower 仓库
  - yarn.lock 能够锁定安装的版本并提供确定性的依赖关系。不再 rm -rf - node_modules！
  - yarn install 花费的时间是 npm install 的一半（不使用缓存的前提下）
  - 缓存和脱机模式使构建过程几乎不花费时间
- 2016：npm 发布 shrinkwrap🧯
  - 尝试处理依赖项锁定
  - 不幸的是，一些错误和超出其管理能力的承诺导致该工具的声誉下降
- 2017：npm 5 发布🔓
  - package-lock.json 是他们的新工具，shrinkwrap 被放在一边
  - package-lock.json 开始与 yarns 锁定文件竞争
- 2018：npm ci 发布🛬
  - 直接用 package-lock.json 构建代码
  - 没有代价高昂的依赖项安全性分析和版本分析
  - 大大减少了在构建服务器上的构建时间！
- 2018：npm 6 发布👮‍♀️
  - npm 检查要安装的依赖项中的安全漏洞
  - yarn 和 npm 的构建时间不再有显差异
- 2019：tink 开始进入 beta 模式🦋
  - 避免使用 node_modules，而是为项目中的每个依赖项创建一个带有哈希值的文件
  - 尚未做好投入生产环境的准备
- ...

## npm/yarn 的问题
- 在最早期的`npm`版本(npm v2)，`npm`的设计可以说是非常的简单,在安装依赖的时候会将依赖放到` node_modules`文件中; 随着项目的不断增大，依赖逐渐变成一个巨大的依赖树，不同依赖之间重复的依赖包也会重复安装，既占用我们电脑内存，也在安装/删除的过程
中变得极为缓慢， 形成`嵌套地狱`
- 为了解决这些问题，(npm v3)重新考虑了node_modules结构并提出了扁平化。
- 在 (npm v5) 中增加了 `package-lock.json` 文件， 来实现和yarn.lock一样的锁定版本操作

从 npm3 开始，包括 yarn，都着手来通过`扁平化依赖`的方式来解决这个问题。相信大家都有这样的体验，我明明就装个 `express`，为什么 `node_modules`里面多了这么多东西？

类似下面这样:
```
node_modules
├─ foo
|  ├─ index.js
|  └─ package.json
└─ bar
   ├─ index.js
   └─ package.json
```
所有的依赖都被拍平到`node_modules`目录下，不再有很深层次的嵌套关系。这样在安装新的包时，根据 node require 机制，会不停往上级的`node_modules`当中去找，如果找到相同版本的包就不会重新安装，解决了大量包重复安装的问题，而且依赖层级也不会太深。

但是， 扁平化的方式依然存在诸多问题

例如：

1、依赖结构的不确定性， 
  - 由于扁平化会将一些依赖中依赖的包安装到同级
  - 将会存在某些包提升同级的不确定性
`
2、扁平化算法复杂度高，耗时长

3、项目中仍然可以非法访问没有声明过依赖的包
  - 对于一个安装包内 `package.json` 中未申明的包，npm/yarn 由于扁平化的原因， 可以借助其安装的包内使用的依赖直接使用，这对于维护来说极度不安全， 当其依赖去除或升级， 将不可控
    - 例如，dui 中使用的 `moment.js`, 随着后面可能的升级， 假如将其替换为`day.js`,将导致代码报错
  - 在很多时候， 我们安装一个依赖， 在`node_modules`中存在一堆乱七八糟的依赖，极度影响排查问题

## 大胆设想

aa：我们来YY一下新的`node_modules`结构吧，怎么让`node_modules`看起来更干净呢？
bb：我们项目中使用了 `react`、`@dji/dui` 两个包，能不能在里面只显示这两个包的依赖呀！
aa：那这两个包所需的依赖怎么办呢？
bb：要不搞个隐藏文件放起来，并且不嵌套，用链接连起来，每个包用版本号区分开就好了
aa：那我们怎么超过 npm/yarn 的速度呢？
bb：我们用硬链接吧，即速度超过了他们，还省磁盘空间了


## pnpm - 一个新的包版本管理解决方案
[平铺的结构不是 node_modules 的唯一实现方式](https://pnpm.io/zh/blog/2020/05/27/flat-node-modules-is-not-the-only-way)

### 什么是pnpm
`pnpm` - 高性能 npm

### 特性概览
**1、速度快**
pnpm 安装包的速度究竟有多快？我们可以从 `pnpm` 的官方文档中找到答案

| action  | cache | lockfile | node_modules| npm | pnpm | Yarn | Yarn PnP |
| ---     | ---   | ---      | ---         | --- | --- | --- | --- |
| install |       |          |             | 51s | 14.4s | 39.1s | 29.1s |
| install | ✔     | ✔        | ✔           | 5.4s | 1.3s | 707ms | n/a |
| install | ✔     | ✔        |             | 10.9s | 3.9s | 11s | 1.8s |
| install | ✔     |          |             | 33.4s | 6.5s | 26.5s | 17.2s |
| install |       | ✔        |             | 28.3s | 11.8s | 23.3s | 14.2s |
| install | ✔     |          | ✔           | 4.6s | 1.7s | 22.1s | n/a |
| install |       | ✔        | ✔           | 6.5s | 1.3s | 713ms | n/a |
| install |       |          | ✔           | 6.1s | 5.4s | 41.1s | n/a |
| update  | n/a   | n/a      | n/a         | 5.1s | 10.7s | 35.4s | 28.3s |

![Graph of the alotta-files results](https://github.com/pnpm/benchmarks-of-javascript-package-managers/raw/main/results/imgs/alotta-files.svg)

从上图数据中可以看出， 在pnpm面前， npm和yarn 一个能打的都没有。
在绝多大数场景下，包安装的速度都是明显优于 npm/yarn，速度会比 npm/yarn 快 2-3 倍。

**2、高效利用磁盘空间**

pnpm 内部使用`基于内容寻址`的文件系统来存储磁盘上所有的文件，这个文件系统出色的地方在于:

- 不会重复安装同一个包。用 npm/yarn 的时候，如果 100 个项目都依赖 lodash，那么 lodash 很可能就被安装了 100 次，磁盘中就有 100 个地方写入了这部分代码。但在使用 pnpm 只会安装一次，磁盘中只有一个地方写入，后面再次使用都会直接使用 `hardlink`(硬链接)。
- 即使一个包的不同版本，pnpm 也会极大程度地复用之前版本的代码。举个例子，比如 lodash 有 100 个文件，更新版本之后多了一个文件，那么磁盘当中并不会重新写入 101 个文件，而是保留原来的 100 个文件的 `hardLink`，仅仅写入那`一个新增的文件`。

```
硬连接测试
创建两个相同的项目 `npm-yarn-pnpm`、`npm-yarn-pnpm-hardLink`
分别用pnpm 安装依赖 `pnpm install`
同时到其中一个包， 例如 `react-router`
`cd node_modules/react-router`
`ls -li` 查看文件id
```

![image-20220505021043812](./WechatIMG204.png)

**3. 支持 monorepo**
[monorepo](https://www.perforce.com/blog/vcs/what-monorepo)

**4. 安全性高**
之前在使用 npm/yarn 的时候，由于 node_module 的扁平结构，如果 A 依赖 B， B 依赖 C，那么 A 当中是可以直接使用 C 的，但问题是 A 当中并没有声明 C 这个依赖。因此会出现这种非法访问的情况。但 pnpm 脑洞特别大，自创了一套依赖管理方式，很好地解决了这个问题，保证了安全性

### 使用
说了这么多，估计你会觉得 `pnpm` 挺复杂的，是不是用起来成本很高呢？
恰好相反，pnpm 使用起来十分简单，如果你之前有 npm/yarn 的使用经验，甚至可以无缝迁移到 pnpm 上来。不信我们来举几个日常使用的例子。

#### pnpm install
跟 npm install 类似，安装项目下所有的依赖。但对于 monorepo 项目，会安装 workspace 下面所有 packages 的所有依赖。不过可以通过 --filter 参数来指定 package，只对满足条件的 package 进行依赖安装。
当然，也可以这样使用，来进行单个包的安装:

```js
// 安装 axios
pnpm install axios
// 安装 axios 并将 axios 添加至 devDependencies
pnpm install axios -D
// 安装 axios 并将 axios 添加至 dependencies
pnpm install axios -S
复制代码
```

当然，也可以通过 --filter 来指定 package。

#### pnpm update
根据指定的范围将包更新到最新版本，monorepo 项目中可以通过 --filter 来指定 package。

#### pnpm uninstall
在 node_modules 和 package.json 中移除指定的依赖。monorepo 项目同上。举例如下:
```
// 移除 axios
pnpm uninstall axios --filter package-a
```

<!-- ### 依赖管理 -->
<!-- ### hard link -->

--
面对 npm / yarn / pnpm， 可能我们需要根据不同场景去选择不同的工具来更高效开发， 所以就有了 `ni` 
--

## ni
### 前言
当我们看 [vue3仓库](https://github.com/vuejs/core/blob/main/.github/contributing.md#development-setup) 时， 发现 vue3 建议使用 `pnpm` 来安装依赖， 并推荐安装 `ni` 以帮助在不同的包版本管理器之间切换。

### 特点
- 使用`TypeScript`作为开发语言
- 核心代码仅仅一百多行

### ni做了什么
1. 根据锁文件猜测用哪个包管理器 npm/yarn/pnpm - [detect 函数](https://github.com/antfu/ni/src/detect.ts)
2. 抹平不同的包管理器的命令差异 - [parseNi 函数](https://github.com/antfu/ni/src/commands.ts)
3. 最终运行相应的脚本 - [execa 工具](https://github.com/sindresorhus/execa)
<!-- 
1. 找到项目根路径下的锁文件。返回对应的包管理器 `npm/yarn/pnpm`。
2. 如果没找到，那就返回 `null`。
3. 如果找到了，但是用户电脑没有这个命令，则询问用户是否自动安装。 
-->

### 使用
全局安装
```shell
npm i -g @antfu/ni
```
install
```shell
ni
# npm install
# yarn install
# pnpm install
```
add
```shell
ni axios
# npm i axios
# yarn add axios
# pnpm add axios
```

### 猜一猜
**如果package-lock.json,yarn.lock,pnpm-lock.yaml都存在的话，按哪个执行呢？**

```ts
// ni/src/agents.ts
export const LOCKS: Record<string, Agent> = {
  'pnpm-lock.yaml': 'pnpm',
  'yarn.lock': 'yarn',
  'package-lock.json': 'npm',
}
```

### 总结
从`ni`工具来看，一百来行代码可以实现 npm、yarn、pnpm 工具的自定义， 我们可以借鉴它来实现自己的shell工具自定义包， 下一次，让我们来试着实现一个类似的包

**尽情期待。。。。**



## 其他

- [npm](./npm-yarn-pnpm/doc/npm.md)
- [yarn](./npm-yarn-pnpm/doc/yarn.md)
- [pnpm](./npm-yarn-pnpm/doc/pnpm.md)
- [ni](./npm-yarn-pnpm/doc/ni.md)