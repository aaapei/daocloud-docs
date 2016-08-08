---
title: 'Dockerfile 注意事项和高级功能'
taxonomy:
    category:
        - docs
---

<!-- reviewed by fiona -->

## Dockerfile最佳实践

与使用的其他任何应用程序一样，总会有可以遵循的最佳实践。你可以阅读更多有关 Dockerfile 的最佳实践。以下是我们列出的基本的 Dockerfile 最佳实践：

- 保持常见的指令像 MAINTAINER 以及从上至下更新 Dockerfile 命令。
- 当构建镜像时使用可理解的标签，以便更好地管理镜像。
- 避免在 Dockerfile 中映射公有端口。
- CMD 与 ENTRYPOINT 命令请使用数组语法。

### DaoCloud 上的 Dockerfile 编写注意事项

DaoCloud 通过读取 Dockerfile 内容，和来自代码仓库的源代码，为用户构建 Docker 镜像。由于众所周知的原因，国内访问 Docker Hub 的速度令人无法忍受，因此国内常规网络环境下的 Docker 镜像构建速度非常缓慢。DaoCloud 采用非常先进的全球分布式构建引擎，有效缓缓解国内网络问题带来的构建延迟。DaoCloud 兼容 Dockerfile 的所有格式，但是有以下几个注意事项，需要开发者知晓：

- 如您在 Dockerfile 中需要更新 Linux 组件，或安装编程语言的依赖包等，请**不要使用国内源**，请使用您的 Linux 发行版和编程语言分发机制提供的默认更新源。
- 您可以在构建过程中看到完整的日志文件，如果构建出现问题，日志文件是排错的首选方式。
- 考虑到您的镜像会频繁构建，我们在构建服务器端开启了缓存，之前构建过的 Docker Image Layer 不会重新执行构建，完成和传输的速度也会更快。
- 我们设定了一个构建超时的时间。对于免费用户，构建时间上限是 1 小时，如果 1 小时内您的镜像构建仍未完成（通常是遇到构建问题并死锁），系统将取消您的构建任务；对于付费用户，这个超时时限是 12 小时。