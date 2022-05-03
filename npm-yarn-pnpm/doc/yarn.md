# yarn
## 知识点
- yarn 1
- yarn 2
- monorepor
- lerna
- pnp

## yarn 1 优势
- 速度快
  - 并行安装：无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装。而 Yarn 同步执行所有任务，提高了性能。
  - 离线模式：如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了。
- 安装版本统一
  - 为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，Yarn 就会创建（或更新）yarn.lock 这个文件。这么做就保证了，每一次拉取同一个项目依赖时，使用的都是一样的模块版本。
- 更好的语义化
  -  yarn改变了一些npm命令的名称，比如 yarn add/remove，感觉上比 npm 原本的 install/uninstall 要更清晰。

## 问题
- Yarn 2不再读取npm的配置

## 参考资料
- [yarn 1 文档](https://classic.yarnpkg.com/lang/en/)
- [yarn 2 文档](https://yarnpkg.com/getting-started/migration)
- [Yarn 2尝鲜](https://juejin.cn/post/6896447858841681928)
- [字节的一个小问题 npm 和 yarn不一样吗？](https://juejin.cn/post/7060844948316225572)
