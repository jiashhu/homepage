---
title: '本地调试部署网页'
date: 2025-01-16
tags:
  - 文档
  - 技术
---

### 如何本地调试

#### 使用 Docker

Docker 是一个用于创建和管理容器化应用程序的平台。以下是如何使用 Docker 来运行 Jekyll 网站的步骤：

1. **构建容器**：
   使用 `docker build` 命令构建 Docker 镜像。这个命令会读取当前目录中的 Dockerfile，并根据其中的指令创建一个新的 Docker 镜像。`-t jekyll-site` 选项用于为镜像指定一个标签（名称）。

   ```sh
   docker build -t jekyll-site .
   ```

2. **运行容器**：
   使用 `docker run` 命令运行 Docker 容器。`-p 4000:4000` 选项将主机的 4000 端口映射到容器的 4000 端口，`--rm` 选项表示容器在停止后会自动删除，`-v $(pwd):/usr/src/app` 选项将当前目录挂载到容器中的 `/usr/src/app` 目录，`jekyll-site` 是要运行的镜像名称。

   ```sh
   docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
   ```

3. **项目依赖**：
   项目依赖通常指的是项目运行所需的外部库、工具或其他资源。在 Jekyll 项目中，项目依赖包括 Gemfile 中指定的 Ruby gems 以及其他配置文件。

   每次修改 Dockerfile 或项目依赖时，通常需要重新构建镜像。但如果镜像已经存在且没有变化，你可以直接运行容器，而不需要每次都重新构建。

4. **更新内容**：
   如果你更新了网页内容（如 Markdown 文件）或 `_config.yml` 文件，这些更改通常不需要重新构建 Docker 镜像。你只需重新运行容器即可，因为这些文件会通过挂载到容器中。

#### 遇到的问题

* **网页显示不正确**：可能是目录路径不正确。

#### 参考

* 使用 Docker（参考 [https://github.com/academicpages/academicpages.github.io](https://github.com/academicpages/academicpages.github.io)）

#### MacOS 的使用

在 Docker Desktop 中，如果已经有了 `jekyll-site` 镜像，你可以直接运行它，而不需要重新构建。只需执行 `docker run` 命令即可。

```sh
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site