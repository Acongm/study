# ni
## 前言
当我们看 [vue3仓库](https://github.com/vuejs/core/blob/main/.github/contributing.md#development-setup) 时， 发现 vue3 建议使用 `pnpm` 来安装依赖， 并推荐安装 `ni` 以帮助在不同的包版本管理器之间切换。

## 特点
- 使用`TypeScript`作为开发语言
- 核心代码仅仅一百多行

## ni做了什么
1. 根据锁文件猜测用哪个包管理器 npm/yarn/pnpm - [detect 函数](https://github.com/antfu/ni/src/detect.ts)
2. 抹平不同的包管理器的命令差异 - [parseNi 函数](https://github.com/antfu/ni/src/commands.ts)
3. 最终运行相应的脚本 - [execa 工具](https://github.com/sindresorhus/execa)
<!-- 
1. 找到项目根路径下的锁文件。返回对应的包管理器 `npm/yarn/pnpm`。
2. 如果没找到，那就返回 `null`。
3. 如果找到了，但是用户电脑没有这个命令，则询问用户是否自动安装。 
-->

## 使用
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

## 猜一猜
**如果package-lock.json,yarn.lock,pnpm-lock.yaml都存在的话，按哪个执行呢？**

```ts
// ni/src/agents.ts
export const LOCKS: Record<string, Agent> = {
  'pnpm-lock.yaml': 'pnpm',
  'yarn.lock': 'yarn',
  'package-lock.json': 'npm',
}
```

## 总结
从`ni`工具来看，一百来行代码可以实现 npm、yarn、pnpm 工具的自定义， 我们可以借鉴它来实现自己的shell工具自定义包， 下一次，让我们来试着实现一个类似的包

**尽情期待。。。。**
