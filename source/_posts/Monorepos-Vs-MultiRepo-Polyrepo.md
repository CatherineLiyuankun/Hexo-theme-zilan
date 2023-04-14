---
title: Monorepos Vs MultiRepo/Polyrepo
catalog: true
date: 2023-04-14 10:05:29
subtitle:
header-img:
tags:
---

# What is a Monorepo?

[What is a Monorepo?](https://monorepo.tools/#what-is-a-monorepo)

# Why Monorepo

[Why Monorepo](https://monorepo.tools/#why-a-monorepo)

Monorepo是指将所有项目模块都存放在一个代码库中的做法。通常，我们会为每个项目模块建立一个独立的代码库，但是在一些特殊情况下，将所有项目模块放在一个代码库中会更加方便。通常情况下，Monorepo都会配合一些特殊的工具使用，比如Lerna、Yarn Workspaces、Bazel等。

## MultiRepo Vs MonoRepo

# Monorepo的优缺点

## 优点

- 模块复用性更高：在Monorepo中，所有的模块都在同一个代码库中，这意味着所有的模块可以互相依赖，相互调用，模块复用性更高，避免了重复开发。
- 代码可维护性更高：Monorepo可以使得所有项目模块在一个仓库中，开发人员可以更加方便的进行代码的维护和修改，同时也可以提高开发效率。
- 更容易进行代码重构：Monorepo使得整个项目的代码都在一个仓库中，因此进行代码重构时，更加方便。

## 缺点

- 代码库体积变大：将所有的项目模块都放在一个代码库中，会导致代码库体积变大，同时代码库的构建时间和编译时间也会相应变长。
- 部署复杂度增加：在Monorepo中，所有的模块都在同一个代码库中，一旦有代码发生变动，所有的模块都需要重新构建和部署，因此部署复杂度增加。

# Monorepo的应用场景

- 多个项目共用同一组件：如果不使用Monorepo，那么每个项目都需要维护一份组件库，不仅工作量大，而且还容易出现版本管理问题。使用Monorepo可以将所有的组件都放在一个代码库中，避免了重复维护和版本管理问题。
- 多个项目依赖同一份代码：如果有多个项目依赖同一份代码，那么如果不使用Monorepo，这些项目都需要去维护自己的一份代码库，使用Monorepo可以避免重复维护的问题。
- 代码拆分成多个模块：如果一个项目的代码越来越复杂，代码行数越来越多，那么可以考虑将代码拆分成多个模块，使用Monorepo可以更加方便的进行代码拆分和管理。
- 提高代码共享和复用：使用Monorepo可以将代码库中的模块复用在


<details>
  <summary>对比表格 (点击展开)</summary>
  <p>
```markdown
|                     | MultiRepo | MonoRepo   |
| ------------------- | -------------------- | --------------- |
| Pros  |  <br> - Enables better tracking of changes and version control.- Allows for independent release cycles for different projects.- Can lead to faster build times as only the necessary code needs to be built.- Reduces the risk of a single point of failure.     |  <br> - Easier **dependency management** as all code is in one repository.<br> - **One version of everything** No need to worry about incompatibilities because of projects depending on conflicting versions of third party libraries.<br> - Allows for **sharing** **of code** and resources between projects.<br> - Atomic commits across projects Everything works together at every commit. There's no such thing as a breaking change when you fix everything in the same commit.<br> - **Simplifies build and release** processes.<br> - Developer mobility Get a consistent way of building and testing applications written using different tools and technologies. Developers can confidently contribute to other teams’ applications and verify that their changes are safe.<br> - Can lead to better **code consistency** and easier maintenance.- Enables better **code reuse and refactoring**. Allows for better **collaboration** between teams.<br> - **No overhead to create new projects** Use the existing CI setup, and no need to publish versioned packages if all consumers are in the same repo.    <br> - **Hard-to-see-affected applications:** Once a developer made an update to a component library, it was hard to see all affected applications company-wide, which usually resulted in breaking features.    <br> - **Hard mode onboarding:** Newcomers struggled to find related components in these multiple codebases. |
| Cons |  <br> - Can be more complex to **manage dependencies** between different repositories.<br> - **Costly cross-repo changes to shared libraries and consumers**       Consider a critical bug or breaking change in a shared library: the developer needs to set up their environment to apply the changes across multiple repositories with disconnected revision histories. Not to speak about the coordination effort of versioning and releasing the packages.<br> - Can make it harder to **share code and resources** between projects.<br> - **Cumbersome code sharing** To share code across repositories, you'd likely create a repository for the shared code. Now you have to set up the tooling and CI environment, add committers to the repo, and set up package publishing so other repos can depend on it. And let's not get started on reconciling incompatible versions of third party libraries across repositories...<br> - Can lead to **inconsistencies** in code and maintenance issues.<br> - **Inconsistent tooling**       Each project uses its own set of commands for running tests, building, serving, linting, deploying, and so forth. Inconsistency creates mental overhead of remembering which commands to use from project to project.<br> - Can create **silos** between different **teams** working on different repositories.<br> - **Significant code duplication** - No one wants to go through the hassle of setting up a shared repo, so teams just write their own implementations of common services and components in each repo. This wastes up-front time, but also increases the burden of maintenance, security, and quality control as the components and services change. |  <br> - Can be difficult to set up and maintain.- Can lead to slower build times as the entire repository needs to be rebuilt.- Can make it harder to track changes and version control.- Can create a single point of failure.               |
| Use Cases  |  <br> - Large-scale projects with **multiple independent** projects.- Projects with **complex dependencies or different release** cycles.- Teams with independent developers working on different codebases.                |  <br> - Large-scale enterprise projects with **multiple interdependent** projects.- Projects with **shared dependencies** or code.- Teams with multiple developers working on the same codebase.      |
```
  </p>
</details>

## MonnoRepo 解决了什么问题

## MonnoRepo 又引入了什么问题

## MonnoRepo 工具解决了哪些问题

# Monorepo features

- [Monorepo features](https://monorepo.tools/#monorepo-features)

# Monorepos tool comparison

Compare [Bazel (by Google),  Gradle Build Tool (by Gradle, Inc),  Lage (by Microsoft),  Lerna, Nx (by Nrwl), Pants (by the Pants Build community), Rush (by Microsoft), and Turborepo (by Vercel)](https://monorepo.tools/#tools-review).

There are so many awesome Monorepo tools, software and architectures.

Some enterprise-level solutions, such as Google's Bazel and Gradle, have little to do with the front end, and the cost of getting started is relatively high, so we will not discuss them here.

| Monorepo Solution | Introduction        | **company* <br> -   | URL | Pros    | Cons      | Pricing| Ease of Use    | Scalability         | Compatibility  | Dependency Management | Task Runner | Version Management |
| ----------------- | ------- | ------------------ | ------------- | ------------- | --------------- | --------------------- | -------------- | ------------------- | ------ | --------------------- | ----------- | ------------------ |
| Yarn Workspaces   | A package manager for JavaScript that allows you to manage multiple packages within a single monorepo.  | Opensource      | [![](https://yarnpkg.com/favicon-32x32.png?v=775b53071ebde4f6d738805a2d9fcb72)Workspaces](https://yarnpkg.com/features/workspaces)      | Easy to set up and use, with clear documentation and a simple CLI.           | Can become slow and unwieldy with a highly complex or deeply nested dependency graph.            | Free and open source. | Easy           | Medium to Large     | Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries. Can be used with npm packages as well.  | Yes    | No          | No  |
| pnpm              | [pnpm](https://pnpm.js.org/en/ "https://pnpm.js.org/en/") is a JavaScript dependency management tool that supports monorepos through a set of dedicated commands called `pnpm multi`.    | Opensource      | [![](https://pnpm.io/img/favicon.png)Fast, disk space efficient package manager | pnpm](https://pnpm.io/)     | Offers fast and efficient package management, with support for multiple registries and package sources.       | May not provide the same level of customization or tooling as some other solutions.              | Free and open source. | Easy           | Medium to Large     | Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries.        | Yes    | No          | No  |
| Lerna             | [Lerna](https://lerna.js.org/ "https://lerna.js.org/") is a tool for managing JavaScript projects with multiple packages, built on Yarn. | Opensource [**recently changed stewardship to Nrwl**](https://github.com/lerna/lerna/issues/3121 "https://github.com/lerna/lerna/issues/3121")**!** | [![](https://github.com/fluidicon.png)GitHub - lerna/lerna: Lerna is a fast, modern build system for managing and publishing multiple JavaScript/TypeScript packages from the same repository.](https://github.com/lerna/lerna) | Offers a wide range of features and customization options. Supports large-scale projects with a highly complex or deeply nested dependency graph.         | Can be complex to set up and configure, with a steeper learning curve than some other solutions. | Free and open source. | Medium         | Large| Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries. Can be used with npm packages as well.  | Yes    | No          | Yes |
| Nx | [Nx](https://nx.dev/ "https://nx.dev/") is a build system for TypeScript monorepos and a set of monorepo management tools.        | Nrwl            | [![](https://nx.dev/favicon/favicon-16x16.png)Nx: Smart, Fast and Extensible Build System](https://nx.dev/)   | Offers a comprehensive set of tools and features for managing monorepos, including testing, linting, and deployment. Can be used with a wide range of languages and frameworks. | May require some additional configuration and setup for certain workflows. | Free and open source. | Easy to Medium | Large| Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries. Integrates with popular development tools like VS Code, Git, and Docker. | Yes    | Yes         | Yes |
| Turborepo         | [Turborepo](https://turborepo.org/ "https://turborepo.org/") is a high-performance build system for JavaScript and TypeScript codebases. | Vercel          | [![](https://cdn0.dan.com/assets/icons/favicon-8f8be32076803305bd39913d14e9f28567adc474d60a95af6e0d21282302ce6a.ico)turborepo.dev - Domain Name For Sale | Dan.com](https://turborepo.dev/)    | Offers fast and scalable builds, with automatic caching and parallelization. Supports multiple languages and frameworks. | Relatively new and may have some limitations or issues not yet discovered. | Free and open source. | Easy           | Large| Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries.        | Yes    | Yes         | Yes |
| Rush              | [Rush Stack](https://rushstack.io/ "https://rushstack.io/") is a family of tools geared towards large scale TypeScript monorepos, and based around the [Rush](https://rushjs.io/ "https://rushjs.io/") build orchestrator | Microsoft       | [![](https://rushjs.io/images/site/favicon.ico)Rush](https://rushjs.io/)     | Offers advanced features like incremental builds and parallel testing, with support for multiple package managers and deployment targets.      | Can be complex to set up and configure, with a steeper learning curve than some other solutions. | Free and open source. | Medium         | Large to Very Large | Fully compatible with React, TypeScript, and other popular JavaScript frameworks and libraries. Can be used with npm packages as well.  | Yes    | Yes         | Yes |

# Monorepo 技术框架迭代

[Monorepo 的过去、现在、和未来](https://zhuanlan.zhihu.com/p/504554070)

## Lerna + Yarn Workspace (Most used before)

## PNPM Workspace (New package management)

## Nx Vs Turborepo Vs Rush (New monorepo solution)

### What’s the problem with the previous solution?

### Monorepo Framework

### Nx and Turborepo

# Resources

## [Monorepo 视频和播客](https://monorepo.tools/#monorepo-videos-podcasts)

这里收集了一些有关 Monorepo 的视频和播客。

- [Using Yarn Workspaces and Lerna with TypeScript Mono-repos](https://www.youtube.com/watch?v=6pCBU6QSfEQ) - TypeScript 作者之一, Ryan Cavanaugh 在 React Europe 2018 上的演讲，介绍了如何使用 Yarn Workspaces 和 Lerna 来构建 TypeScript monorepo。
- [Monorepos: Simplify Your Development Life!](https://www.youtube.com/watch?v=SSNrW8EXvR0) - 由 Kent C. Dodds 主持的视频，介绍了使用 Yarn Workspaces 和 Lerna 创建 monorepo 的基础知识。
- [The Benefits of Monorepos for React Native and Web Projects](https://www.youtube.com/watch?v=Ys3hZNJwHzk) - 由 Callstack 公司的 Eric Vicenti 主持的演讲，讨论了如何使用 monorepo 来改进 React Native 和 Web 项目的开发流程。
- [Scaling your Codebase with Nx and Monorepos](https://www.youtube.com/watch?v=7IkUgCLr5oA) - Nrwl 公司的 Jeff Cross 主持的演讲，介绍了如何使用 Nx 来扩展 monorepo 项目，并讨论了如何处理大型代码库的挑战。
- [Monorepo Patterns for Node.js and TypeScript Applications](https://www.youtube.com/watch?v=d0E2KWD4YxE) - Node.js 开发人员 Wes Todd 主持的视频，讲解了如何使用 monorepo 来组织和构建 Node.js 和 TypeScript 应用程序。
- [Monorepo Architecture for Frontend Projects](https://www.youtube.com/watch?v=1Y-PqBH-htk) - 前端工程师 Karol Wrótniak 主持的演讲，介绍了如何使用 monorepo 构建现代 Web 应用程序，以及如何处理不同项目之间的共享代码和依赖关系。

## Monorepo articles

Here is a curated list of articles about monorepos that we think will greatly support what you just learned.

- [The One Version Rule – opensource.google](https://opensource.google/docs/thirdparty/oneversion?utm_source=monorepo.tools)
- [Why TurboRepo Will Be The First Big Trend of 2022](https://dev.to/swyx/why-turborepo-will-be-the-first-big-trend-of-2022-4gfj?utm_source=monorepo.tools)
- [Build Monorepos, Not Monoliths – dev.to](https://dev.to/agentender/build-monorepos-not-monoliths-4gbc?utm_source=monorepo.tools)

## [Monorepos Books](https://monorepo.tools/#monorepo-books)

- [Effective React Development with Nx](https://f.hubspotusercontent20.net/hubfs/2757427/effective-react-with-nx-2022.pdf)
