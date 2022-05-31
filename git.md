# Git 管理规范

## 目录

1. [配置 SSH](#配置SSH)
1. [工作流程](#工作流程)
1. [Branch 规范](#Branch规范)
1. [Commit 规范](#Commit规范)
1. [Tag 规范](#Tag规范)
1. [Push 规范](#Push规范)
1. [使用技巧](#使用技巧)
1. [管理工具](#管理工具)
1. [使用 merge、rebase、cherry-pick](#使用merge_rebase_cherry-pick)

<a id="配置SSH"></a>

## 配置 SSH

在开始前，请先配置本地的 ssh 环境，然后将公钥配置到 GitLab/Github 的 Setting > SSH Keys 中

这样可以通过 ssh 来管理推送，避免在后续的 git 操作中频繁输入 git 账号与密码。

```bash
# 基于邮箱生成ssh key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# 查看本机公钥
cd ~ && cat .ssh/id_rsa.pub
```

后续 clone 时推荐使用 ssh 链接

**[⬆ 返回顶部](#目录)**

<a id="工作流程"></a>

## 工作流程

<img src="https://raw.githubusercontent.com/yangin/code-assets/main/code-style-guide/git/1-1-1.png">

**[⬆ 返回顶部](#目录)**

<a id="Branch规范"></a>

## Branch 规范

### 使用规范

1. 每当开始一个新的任务时，需要从目标仓库切一个 branch 出来，作为自己的工作空间。

2. 每当结束一个阶段的开发时，在代码合并后要及时删除 branch。

<br/>

### 命名规范

分支命名需以英文命名，如非必要，禁止使用拼音。

当描述需要多个单词，以下划线（\_）进行连接，如 yj_richtext。

<br/>

#### 特殊分支命名规范

主分支：master

测试环境分支：test

开发环境分支：dev

<br/>

#### 商户生产分支命名规范

格式：master\_<商户名称简拼（ <=2 个字）或全拼（ >2 个字）>

参考：master_hsxcb（华师宣传部）、master_beiqi（北汽）

<br/>

#### 开发分支命名规范

场景：开发新的需求或修复线上的 bug

格式：dev*<项目名称或简称>[*<目的>]

参考：dev_lecture（会议讲座）、dev_lecture_fix（会议讲座的 bug 修复）

<br/>

#### 个人分支命名规范

场景：个人临时分支，用来做备份等

格式：<姓名简称>_<项目名称或简称>[_<目的>]

参考：yj_hs、yj_hs_richtext

**[⬆ 返回顶部](#目录)**

<a id="Commit规范"></a>

## Commit 规范

### 使用规范

1. 原则上是处理一个需求，提交一个 commit,若同时处理了多个问题，需要将 commit 拆成多个来提交

2. commit message 以单行文字简短描述，能描述清楚改动内容。

3. 推荐采用 rebase 来进行本地 commit log 管理， 避免不必要的 merge 记录。

<br/>

### 编写规范

#### commit 文本格式

```bash
<type>: description
```

type 代表某次提交的类型，如 FIX、FEAT 等, 注意冒号后有一个英文空格

description 推荐为中文，必要关键字或表达需要情况下使用英文

<br/>

#### type 类型

`RELEASE`: 升级 version

`CHORE`: 改变构建流程、或增加依赖库、继承测试等

`DOCS`: 仅修改了文档，如 README、CHANGELOG 等

`FEAT`: 添加一个新功能

`FIX`: 修复 Bug

`PERF`: 优化相关，比如提升性能、体验

`REFACTOR`: 代码重构，没有加新的功能或修复 bug

`STYLE`: 仅修改了空格、格式缩进、代码排版等，不改变代码逻辑

`TEST`: 测试用例，包括单元测试、集成测试等

**[⬆ 返回顶部](#目录)**

<a id="Tag规范"></a>

## Tag 规范

基本遵循 [Semver](https://semver.org/lang/zh-CN/) 规范，并稍微做了点调整。

### 编写规范

#### master 分支 tag 规范

格式： major.minor.patch

如：1.0.0

<br/>

#### 子项目分支 tag 规范

格式：major.minor.patch-<项目名>[.<序号>]

如： 1.0.0-hsxc、1.0.0-hsxc.1

<br/>

#### 测试版本 tag 规范

格式：major.minor.patch-dev[.<序号>]

如： 1.0.0-dev、1.0.0-dev.1

<br/>

#### 业务项目规范

major(主版本号): 当项目产生一个阶段性的升级（如底层框架重构，开发了一个大的功能项，产品需要等）时新增，升级时，前后端需同时升级，保持版本号对齐。

minor(次版本号): 当前后端的修改对对方产生影响时（如开发一个新功能，后端修改了接口参数等），需要同步升级，并保持版本号对齐。

patch(修订号): 当前后端对项目做了新的功能或 bug fix 时，且对对象没有影响时 新增。

<br/>

总结：前后端的 major.minor 需始终保持对齐，patch 随自己的项目需求走。部署时，保持 major.mino 对齐即可。

<br/>

#### 工具库规范

major(主版本号):当做了不兼容的 API 修改，

minor(次版本号):当做了向下兼容的功能性新增，

patch(修订号):当做了向下兼容的问题修正。

<br/>

#### 使用说明

标准的版本号只能基于 master 分支打版本

**[⬆ 返回顶部](#目录)**

<a id="Push规范"></a>

## Push 规范

1. 原则上当出现 push 冲突时，严禁强行 push，需处理好冲突后再 push。

2. push 前请 code review 自己的改动，避免 push 时携带一些测试数据，而导致的上线问题。因为 push 后所引起的修改

**[⬆ 返回顶部](#目录)**

<a id="使用技巧"></a>

## 使用技巧

#### 根据作者查询 git log

格式：git log --author=[author]

```bash
git log --author=yangjin
```

#### 根据 commit message 查询 log

格式：git log --grep=[commit-message]

```bash
git log --grep=PDF
```

**[⬆ 返回顶部](#目录)**

<a id="管理工具"></a>

## 管理工具

[Git-CLI](https://git-scm.com/docs)

[GitHub DeskTop](https://desktop.github.com/)

[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)(VSCode 插件)

**[⬆ 返回顶部](#目录)**

<a id="使用merge_rebase_cherry-pick"></a>

## 使用 merge、rebase、cherry-pick

### [merge](https://git-scm.com/docs/git-merge)

merge 主要用来合并分支，常用操作如下：

```bash
# 合并目标分支到当前分支,会产生一条merge commit
git merge <branch>
```

#### 优点

1. 快速合并分支；
2. 根据最终的版本来统一解决冲突, 解决冲突效率高；

#### 缺点

1. 产生一条额外的 merge commit，影响 log 的整洁与美观；
2. merge commit 干扰 rebase 的使用；
3. 当产生冲突时，无法精准定位到产生冲突的 commit；
4. 无法处理指定部分 commit 的合并；

#### 推荐使用场景

可能存在较多冲突的场景, 如集体分支往另外一个集体分支上合时，推荐使用 merge。

如 master --> 商户分支， master --> test 分支

### [rebase](https://git-scm.com/docs/git-rebase)

rebase 主要实现 2 个功能，变基 与 整理 commit log，常用操作如下：

```bash
# 变基，以指定分支做为当前分支的基座
git rebase <branch>
# 整理 commit log, 当遇到merge记录时，会出现问题，所以避免rebase到merge的commit
git rebase -i head~10
```

#### 优点

1. 可以快速合并分支，且不产生 merge commit，并保持 commit log 干净整洁
2. 其强大的 commit 管理功能，包括删除、提交、排序、整理等，可以让你的 commit 保持更好的逻辑完整性，及美观

#### 缺点

1. 当遇到冲突时，需要逐条解决冲突，效率较低，且更容易出错
2. 遇到 merge commit 时，rebase 会出现问题
3. 无法处理指定部分 commit 的合并。

#### 推荐使用场景

个人开发分支往集体分支(如 test, master)上合并时，推荐使用 rebase。

如 yj_dev --> test, yj_dev --> master

### [cherry-pick](https://git-scm.com/docs/git-cherry-pick)

cherry-pick 为挑选某个（或某些） commit 到当前分支，常用操作如下：

```bash
# 挑选单个commit
git cherry-pick <commit>
# 挑选多个commit
git cherry-pick <commit> <commit>
# 挑选多个连续的commit
git cherry-pick <commit>^..<commit>
```

#### 优点

1. 可以精准的挑选并合并某一条或多条 commit；
2. 当出现冲突时，可以更精准的定位到出现冲突的 commit 与位置；

#### 缺点

1. 在处理多条 commit 时，效率较低，且可能有出现丢失 commit 的风险；
2. 在处理多条 commit 遇到冲突时，需要逐条解决冲突，效率较低，且更容易出错；

#### 推荐使用场景

个人开发分支往集体分支(如 test, master)上合并时，推荐使用 cherry-pick。

如 yj_dev --> test, yj_dev --> master

### 最终目标

1. 保证每一条 commit 内容的逻辑完整性;
1. 在集体往集体合并时，要保证准确性，与更高的 merge 效能;
1. 在个人分支上集体分支时，要保证 commit 的精准性，按需合并;
1. 集体 commit log 的干净整洁, 方便后续的问题跟踪。

### 注意事项

1. 关于个人分支上集体分支，如 test、master 等时，采用 cherry-pick 与 rebase 集合的方式；
2. 个人在开发完需求时，可以通过 rebase -i 来对 commit 内容进行整理，保证每个 commit 内容的逻辑完整性，即一个 commit 完成一个需求。

**[⬆ 返回顶部](#目录)**
