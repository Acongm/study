# 现代包管理器 - npm/yarn/pnpm/ni 的选择

## 什么是pnpm
`pnpm`
## 二、特性概览
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
硬连接
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

## 依赖管理

- [npm](./npm-yarn-pnpm/doc/npm.md)
- [yarn](./npm-yarn-pnpm/doc/yarn.md)
- [pnpm](./npm-yarn-pnpm/doc/pnpm.md)
- [ni](./npm-yarn-pnpm/doc/ni.md)