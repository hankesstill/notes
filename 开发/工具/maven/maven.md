[toc]
## Maven
### 简介
- Maven 翻译为"专家"、"内行"，是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。
- Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。
- Maven 也可被用于构建和管理各种项目，例如 C#，Ruby，Scala 和其他语言编写的项目。
### 功能
- 构建
- 文档生成
- 报告
- 依赖
- CMs
- 发布
- 分发
- 邮件列表
### Maven仓库
- 在 Maven 的术语中，仓库是一个位置（place）。
- Maven 仓库是项目中依赖的第三方库，这个库所在的位置叫做仓库。
- 在 Maven 中，任何一个依赖、插件或者项目构建的输出，都可以称之为构件。
- Maven 仓库能帮助我们管理构件（主要是JAR），它就是放置所有JAR文件（WAR，ZIP，POM等等）的地方。
- Maven 仓库有三种类型：
    1. 本地（local）
    2. 中央（central）
    3. 远程（remote）
### Maven 依赖搜索顺序
当我们执行 Maven 构建命令时，Maven 开始按照以下顺序查找依赖的库：
1. 在本地仓库中搜索，如果找不到，执行第2步，如果找到了则执行其他操作。
2. 在中央仓库中搜索，如果找不到，并且有一个或多个远程仓库已经设置，则执行第4步，如果找到了则下载到本地仓库中以备将来引用。
3. 如果远程仓库没有被设置，Maven 将简单的停滞处理并抛出错误（无法找到依赖的文件）。
4. 在一个或多个远程仓库中搜索依赖的文件，如果找到则下载到本地仓库以备将来引用，否则 Maven 将停止处理并抛出错误（无法找到依赖的文件）。
---
- Maven 阿里云(Aliyun)仓库
- Maven 仓库默认在国外， 国内使用难免很慢，我们可以更换为阿里云的仓库。
- 修改 maven 根目录下的 conf 文件夹中的 settings.xml 文件，在 mirrors 节点上，添加内容如下：
```
<mirrors>
    <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>        
    </mirror>
</mirrors>
```