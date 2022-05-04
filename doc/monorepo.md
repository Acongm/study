# 什么是 Monorepo？
一些开发团队使用 monorepo。有些使用多个存储库。在这里，我们将介绍什么是 monorepo，使用它的好处，以及为什么像谷歌这样的公司使用 monorepo。

## 什么是 Monorepo？为什么你要在乎？

> monorepo（单存储库）是一个存储库，用于存储每个项目的所有代码和资产。

出于多种原因，使用 monorepo 很重要。它创造了单一的事实来源。它使共享代码变得更加容易。它甚至使[重构代码变得更加容易](https://www.perforce.com/blog/vcs/really-save-time-code-refactoring)。

## Monorepo 和 Monolith 的区别

> monorepo 是一个单一的存储库。单体是一个庞大的代码库。

可以在 monorepo 中管理单体应用。但是一个单体也可以分成多个存储库。同样，monorepo 可以与微服务一起使用，而不是单体应用。

在这篇博客中，我们将专注于 monorepo。

## Monorepo 与 Multirepo

> monorepo 将所有内容保存在一个存储库中。一个 multirepo（多个存储库）通常为每个项目提供一个存储库。项目越多，存储库就越多。多仓库也称为多仓库。

那么，哪一个更好呢？您是否应该将所有内容放在一个存储库中？还是应该将它分成多个存储库？

### Monorepo 通常最适合……

#### *能见度*

使用单个存储库可以让您查看每个项目的代码和资产。这可以帮助您管理依赖项。

#### *合作*

单个存储库使协作更容易。这是因为每个人都可以访问代码、文件和资产。因此，开发人员可以共享和重用资产。

#### *速度*

使用单个存储库可以帮助您加速开发。例如，您可以进行原子更改（一个操作可以跨多个项目进行更改）。

### Multirepo 通常最适合……

#### *Git 项目*

*在 Git中大规模* 管理 monorepo永远不会奏效。随着存储库变得越来越大，Git 中的 monorepo 成为一个大问题。因此，如果您有使用 Git 的团队，最好有多个存储库。

> Git 的另一个挑战是 Git 缺乏安全性。了解如何锁定 Git。
>
> [锁定 GIT](https://www.perforce.com/resources/vcs/how-lock-down-git)

#### *开源或第三方项目*

在某些版本控制系统中，您需要多个存储库才能使用开源项目或与第三方团队合作。然后，您可以确保第三方开发人员只能访问他们正在处理的项目。

*（当然，使用 Perforce 版本控制 -* [*Helix Core*](https://www.perforce.com/products/helix-core) *- 您可以使用 monorepo 或 multirepo 执行此操作。您可以将权限限制到文件级别，即使在 monorepo 中也是如此。您甚至可以使用*[*Helix4Git*](https://www.perforce.com/products/helix4git)*将 Git 项目带入您的管道。 )* 

## 那么，Monorepo 是个好主意吗？

对于许多公司来说，使用单声道存储库是一个好主意。您可以将每个团队的所有源代码（和其他文件/数字资产）保存在一个存储库中。这样更容易与大家分享。它还可以帮助您保持单一的事实来源。

在任何提交之后，您的所有开发人员都可以看到和使用新代码。[这有助于避免在基于主干的开发](https://www.perforce.com/blog/vcs/trunk-based-development-or-feature-driven-development)中普遍存在的痛苦合并。

以下是您应该考虑使用单声道存储库的一些原因：

- 你想要一个单一的事实来源。
- 您想轻松共享和重用代码。
- 您希望管理依赖项的可见性（例如，如果您进行更改，还会影响什么？）。
- 您想要进行原子更改（例如，一项操作可以跨多个项目进行更改）。
- 您希望团队进行更多协作。
- 您想要进行大规模更改（例如，[代码重构](https://www.perforce.com/blog/vcs/really-save-time-code-refactoring)）。

如果您决定走 monorepo 路线，那么您将成为很好的伙伴。领先的公司——比如谷歌——使用 monorepo。

## 示例：为什么 Google 使用 Monorepo？

谷歌是众多以使用单一存储库而闻名的大公司之一。

谷歌很早就决定使用 monorepo，并随着公司的发展扩大规模。2015 年，[谷歌 monorepo](https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext)举行：

- 86 TB 的数据。
- 20 亿行代码。
- 900 万个独特的源文件。

那么，为什么 Google 选择 monorepo 并坚持下去呢？因为使用 monorepo 是开放和协作文化的关键。

[Salesforce、Facebook 和 Twitter](https://medium.com/@hoangbkit/why-monorepo-in-2018-89221acd4bfb)也以使用 monorepos 闻名。

当然，如果你选择monorepo，你需要一个可以支持它的VCS。[Helix Core可以支持](https://www.perforce.com/products/helix-core)你 的 monorepo。

## 使用 Helix Core 的 Monorepo 的好处

使用 monorepo 有很多很好的理由。Helix Core 是您的 monorepo 的最佳版本控制。

以下是将 Helix Core 用于您的 monorepo 的 4 个主要好处。

### 力量

Helix Core 是一个强大的版本控制系统。这是实现大规模高性能的最佳选择。

当您在 Helix Core 中有一个 monorepo 时，它可以处理：

- 1,000 名用户中的 10 名（甚至是地理位置分散的团队）。
- 无限的文件。
- PB 级数据。

### 控制

Helix Core 让您可以查看和控制您的 monorepo。事实上，Helix Core 为您提供了两全其美的优势——monorepo 和 multirepo。

例如，multirepo 隔离行为。Monorepo 确保共享责任和可见性。使用 Helix Core，您可以同时获得两者的好处。

您可以使用 Perforce Streams 来隔离分支级别的行为。而且您仍然可以了解跨分支机构的共同责任。

### 安全

Helix Core 是安全的 - 并提供可定制的安全控制。您可以使用[MFA](https://www.perforce.com/blog/vcs/what-is-multi-factor-authentication)等身份验证措施。您可以将访问控制设置为文件级别。

这些安全权限可帮助您在 monorepo 上与第三方开发人员合作。

### 灵活性

Helix Core 非常灵活。您可以使用 Perforce Streams 为您的团队自定义和自动化工作流程。

这有助于您的团队在您的 monorepo 上更好地协作。

您的开发人员将获得快速反馈——以及更快的构建。他们将能够花更少的时间处理工具和流程，而将更多的时间用于交付价值。

### 开始使用 Helix Core

Helix Core 为您提供跨所有项目的单一事实来源。它为您的团队提供权力、控制、安全性和灵活性。

亲自了解 Helix Core 将如何帮助您。您最多可以[免费开始](https://www.perforce.com/products/helix-core/free-version-control)5 位用户。

[获取螺旋核心](https://www.perforce.com/products/helix-core/free-version-control)

 参考资料

- [什么是 Monorepo？](https://www.perforce.com/blog/vcs/what-monorepo)
