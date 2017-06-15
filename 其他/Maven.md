# Maven

### Maven 快速入门
- Maven 介绍<br />
  Maven 是基于项目对象模型（POM），可以通过一小段描述信息来管理项目的构建、报告和文档的软件项目管理工具
- Maven 目录结构
  - src
    - main
      - java
        - package
    - test
      - java
        - package
    - resources

### Maven 核心知识
- Maven 常用的构建命令
  - `mvn -v` 查看 Maven 版本
  - `compile` 编译
  - `test` 测试
  - `package` 打包
  - `clean` 删除 target（target中存放编译好的文件）
  - `install` 安装 jar 包到本地仓库中
- 自动创建目录的两种方式
  1. `archetype:generate` 按照提示进行选择
  2. `archetype:generate -DgroupId=组织名 -DartifactId=项目名-模块名 -Dversion=版本号 -Dpackage=代码所存在的包`
- Maven 中的坐标和仓库
  - 坐标
    ```
    <groupId>com.imooc.maven01</groupId>
    <artifactId>maven01-model</artifactId>
    <version>0.0.1SNAPSHOT</version>
    ```
  - 仓库
    - 本地仓库和远程仓库
    - 镜像仓库
- Maven 生命周期
  - clean   清理项目
  - default 构建项目
  - site    生成项目站点
### Maven 建立 Web 项目
