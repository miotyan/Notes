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
  - clean 清理项目<br />
    三个阶段
    - `pre-clean` 执行清理前的工作
    - `clean` 清理上一次构建生成的所有文件
    - `post-clean` 执行清理后的文件
  - default 构建项目（最核心）<br />
    常用步骤：compile test package install
  - site 生成项目站点<br />
    分为以下阶段：
    - `pre-site` 在生成项目站点前要完成的工作
    - `site` 生成项目的站点文档
    - `post-site` 在生成项目站点后要完成的工作
    - `site-deploy` 发布生成的站点到服务器上
- pom.xml
```
  <!-- 指定了当前pom的版本 -->
  <modelVersion>4.0.0</modelVersion>

  <groupId>反写的公司网址+项目名</groupId>
  <artifactId>项目名+模块名</artifactId>
  <!-- 第一个0表示大版本号
      第二个0表示分支版本号
      第三个0表示小版本号
      后面字母是软件阶段
   -->
  <version>0.0.1-SNAPSHOT</version>

  <!-- 打包方式 jar/war/zip/pom -->
  <packaging>jar</packaging>

  <!-- 项目描述名 -->
  <name>hi</name>
  <!-- 项目地址 -->
  <url>http://maven.apache.org</url>

  <!-- 依赖列表 -->
  <dependencies>
      <!-- 依赖项 -->
      <dependency>
          <groupId></groupId>
          <artifactId></artifactId>
          <version></version>
          <type></type>
          <scope>依赖范围</scope>
          <!-- 设置依赖是否可选 默认false -->
          <optional></optional>
          <!-- 排除依赖传递列表 -->
          <exclusions>
              <exclusion>
              </exclusion>
          </exclusions>
      </dependency>
  </dependencies>

```

### Maven 建立 Web 项目
