# Git管理规范

## 目录

1. [配置SSH](#配置SSH)
1. [工作流程](#工作流程)
2. [Branch规范](#Branch规范)
3. [Commit规范](#Commit规范)
4. [Tag规范](#Tag规范)
5. [Push规范](#Push规范)
6. [使用技巧](#使用技巧)
7. [管理工具](#管理工具)

<a id="配置SSH"></a>

## 配置SSH

在开始前，请先配置本地的ssh环境，然后将公钥配置到 GitLab/Github 的 Setting > SSH Keys 中

这样可以通过ssh来管理推送，避免在后续的git操作中频繁输入git账号与密码。

```bash
# 基于邮箱生成ssh key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
 
# 查看本机公钥
cd ~ && cat .ssh/id_rsa.pub
```

后续clone时推荐使用 ssh 链接

**[⬆ 返回顶部](#目录)**

<a id="工作流程"></a>

## 工作流程

<img src="https://raw.githubusercontent.com/yangin/code-assets/main/code-style-guide/git/1-1-1.png">

**[⬆ 返回顶部](#目录)**

<a id="Branch规范"></a>

## Branch规范

### 使用规范

1. 每当开始一个新的任务时，需要从目标仓库切一个branch出来，作为自己的工作空间。

2. 每当结束一个阶段的开发时，在代码合并后要及时删除branch。

<br/>

### 命名规范

分支命名需以英文命名，如非必要，禁止使用拼音。

当描述需要多个单词，以下划线（_）进行连接，如  yj_richtext。

<br/>

#### 特殊分支命名规范

主分支：master

测试环境分支：test

开发环境分支：dev

<br/>

#### 商户生产分支命名规范

格式：master_<商户名称简拼（ <=2个字）或全拼（ >2个字）>

参考：master_hsxcb（华师宣传部）、master_beiqi（北汽）

<br/>

#### 开发分支命名规范

场景：开发新的需求或修复线上的bug

格式：dev_<项目名称或简称>[_<目的>]

参考：dev_lecture（会议讲座）、dev_lecture_fix（会议讲座的bug修复）

<br/>

#### 个人分支命名规范

场景：个人临时分支，用来做备份等

格式：<姓名简称>_<项目名称或简称>[_<目的>]

参考：yj_hs、yj_hs_richtext

**[⬆ 返回顶部](#目录)**

<a id="Commit规范"></a>

## Commit规范

### 使用规范

1. 原则上是处理一个需求，提交一个commit,若同时处理了多个问题，需要将commit拆成多个来提交

2. commit message以单行文字简短描述，能描述清楚改动内容。

3. 推荐采用 rebase 来进行本地 commit log 管理， 避免不必要的 merge 记录。

<br/>

### 编写规范

#### commit文本格式

```bash
<type>: description
```

type 代表某次提交的类型，如FIX、FEAT等, 注意冒号后有一个英文空格

description 推荐为中文，必要关键字或表达需要情况下使用英文

<br/>

#### type类型

   `RELEASE`: 升级version

   `CHORE`: 改变构建流程、或增加依赖库、继承测试等

   `DOCS`: 仅修改了文档，如README、CHANGELOG等

   `FEAT`: 添加一个新功能

   `FIX`: 修复Bug

   `PERF`: 优化相关，比如提升性能、体验

   `REFACTOR`: 代码重构，没有加新的功能或修复bug

   `STYLE`: 仅修改了空格、格式缩进、代码排版等，不改变代码逻辑

   `TEST`: 测试用例，包括单元测试、集成测试等

**[⬆ 返回顶部](#目录)**

<a id="Tag规范"></a>

## Tag规范

基本遵循 [Semver](https://semver.org/lang/zh-CN/) 规范，并稍微做了点调整。

### 编写规范

#### master分支tag规范

格式： major.minor.patch

如：1.0.0

<br/>

#### 子项目分支tag规范

格式：major.minor.patch-<项目名>[.<序号>]

如： 1.0.0-hsxc、1.0.0-hsxc.1

<br/>

#### 测试版本tag规范

格式：major.minor.patch-dev[.<序号>]

如： 1.0.0-dev、1.0.0-dev.1

<br/>

#### 业务项目规范

major(主版本号): 当项目产生一个阶段性的升级（如底层框架重构，开发了一个大的功能项，产品需要等）时新增，升级时，前后端需同时升级，保持版本号对齐。

minor(次版本号): 当前后端的修改对对方产生影响时（如开发一个新功能，后端修改了接口参数等），需要同步升级，并保持版本号对齐。

patch(修订号): 当前后端对项目做了新的功能或 bug fix时，且对对象没有影响时 新增。

<br/>

总结：前后端的 major.minor 需始终保持对齐，patch 随自己的项目需求走。部署时，保持 major.mino 对齐即可。

<br/>

#### 工具库规范

major(主版本号):当做了不兼容的 API 修改，

minor(次版本号):当做了向下兼容的功能性新增，

patch(修订号):当做了向下兼容的问题修正。

<br/>

#### 使用说明

标准的版本号只能基于master分支打版本

**[⬆ 返回顶部](#目录)**

<a id="Push规范"></a>

## Push规范

1. 原则上当出现push冲突时，严禁强行push，需处理好冲突后再push。

2. push前请code review自己的改动，避免push时携带一些测试数据，而导致的上线问题。因为push后所引起的修改

**[⬆ 返回顶部](#目录)**

<a id="使用技巧"></a>

## 使用技巧

#### 根据作者查询git log

格式：git log --author=[author]

```bash
git log --author=yangjin
```

#### 根据commit message 查询 log

格式：git log --grep=[commit-message]

```bash
git log --grep=PDF
```

**[⬆ 返回顶部](#目录)**

<a id="管理工具"></a>

## 管理工具

[Git-CLI](https://git-scm.com/docs)

[GitHub DeskTop](https://desktop.github.com/)

[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)(VSCode插件)

**[⬆ 返回顶部](#目录)**
