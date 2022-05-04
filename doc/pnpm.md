# pnpm - performant npm

The app's `package.json` [here](https://github.com/pnpm/benchmarks-of-javascript-package-managers/edit/main/fixtures/alotta-files/package.json)

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

## 缺点

- 目前pnpm7 最低支持 node v14.19.1 (需要node较高版本运行环境)
- 对于旧项目存在



## 参考资料
- [Why should we use pnpm?](https://www.kochan.io/nodejs/why-should-we-use-pnpm.html)
- [pnpm 项目](https://github.com/pnpm/sample-project)
- [JavaScript package managers compared: npm, Yarn, or pnpm?](https://blog.logrocket.com/javascript-package-managers-compared/)
- [Pnpm: 最先进的包管理工具](https://zhuanlan.zhihu.com/p/404784010)
- [Flat node_modules is not the only way](https://pnpm.io/blog/2020/05/27/flat-node-modules-is-not-the-only-way)