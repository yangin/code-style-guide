# Git使用规范

*企业采用 [GitLab](http://gitlab.rmny.tech/) 进行代码托管， 仓库地址 <http://gitlab.rmny.tech/>*

*当需要仓库权限时，请联系GitLab管理员（房立俊）*

## 目录

1. [工具](#工具)

1. [工作流](#工作流)

1. [Branch规范](#Branch规范)

1. [Commit规范](#Commit规范)

1. [Push规范](#Push规范)

1. [Tag规范](#Tag规范)

1. [常用命令](#常用命令)

# 工具

[Git-CLI](https://git-scm.com/docs)、 [GitHub DeskTop](https://desktop.github.com/)、[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)(VSCode插件)

# 工作流

*在开始前，请先配置本地的ssh环境，然后将公钥配置到 [GitLab](http://gitlab.rmny.tech/) 的 Setting > SSH Keys 中*

> 这样可以通过ssh来管理推送，避免在后续的git操作中频繁输入git账号与密码。

```bash
# 基于邮箱生成ssh key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 

# 查看本机公钥
cd ~ && cat .ssh/id_rsa.pub 
```

1. 根据项目需求从gitlab上拉取代码仓库

   > 建议使用 ssh 链接

   ```bash
   git clone <仓库地址>
   ```

2. 根据任务目标在本地新建目标分支，如：yj/fix-bugs，作为修改代码仓库
   > 分支名请根据[Branch规范](#branch规范)进行合理命名

   ```bash
   git checkout -b <分支名>
   ```

3. 修改代码后，提交修改内容
   > commit message 须遵从[Commit规范](#commit规范)

   > 原则上要求每完成一个功能需要或修改，提交一个commit，

   > push 须遵从[Push规范](#push规范)

   ```bash
   # 提交代码到暂存区
   git add <修改内容>

   # 添加commit描述
   git commit  -m '[message]'

   # 将本地commit push到gitlab上
   git push

   # 首次提交分支执行
   git push --set-upstream origin <分支名>
   ```

4. 当需要将代码合并到主分支时，需要在gitlab上发起一个 Pull Request（简称PR）, 并将PR的地址发给 review 代码的同事， 通知其 code review 及 合并。

5. 当 review 或者讨论通过后，你的PR被接受，代码会合并到目标分支。

6. 一旦合并到 部署分支（如master等），要及时部署。

# Branch规范

## 使用规范

1. 每当开始一个新的任务时，需要从目标仓库切一个branch出来，作为自己的工作空间。
2. 每当结束一个阶段的开发时，在代码合并后要及时删除branch。

## 命名规范

*分支命名需以英文命名，如非必要，禁止使用拼音。*

*当描述需要多个单词，以中划线（-）进行连接，如  yj/update-rich-text。*

1. 主项目分支命名规范

   格式：<姓名简称>/<功能目的>

   参考：yj/theme、yj/update-rich-text

2. 子项目分支命名规范

   格式：<姓名简称>/<项目名称或简称>[-<目的>]

   参考：yj/hs、yj/hs-update-rich-text

3. 生产/测试/开发分支命名规范

   格式：（prod|test|dev）/<项目名称>

   参考：prod/hs、test/hs、dev/hs

4. 特殊分支命名规范

   主分支：master 或 main

# commit规范

## 使用规范

1. 原则上是处理一个需求，提交一个commit,若同时处理了多个问题，需要将commit拆成多个来提交
2. commit message以单行文字简短描述，能描述清楚改动内容。
3. 推荐采用 [rebase](https://git-scm.com/docs/git-rebase) 来进行 commit log 管理， 避免不必要的 merge 记录。

## 编写规范

1. commit文本格式

   ```bash
      <type>: description
   ```

> type代表某次提交的类型，如FIX、FEAT等, 注意冒号后有一个英文空格

> description推荐为中文，必要关键字或表达需要情况下使用英文

1. type类型

   `RELEASE`: 升级version

   `CHORE`: 改变构建流程、或增加依赖库、继承测试等

   `DOCS`: 仅修改了文档，如README、CHANGELOG等

   `FEAT`: 添加一个新功能

   `FIX`: 修复Bug

   `PERF`: 优化相关，比如提升性能、体验

   `REFACTOR`: 代码重构，没有加新的功能或修复bug

   `REVERT`: 回滚到上一个版本或commit

   `STYLE`: 仅修改了空格、格式缩进、代码排版等，不改变代码逻辑

   `TEST`: 测试用例，包括单元测试、集成测试等

# push规范

   1. 原则上当出现push冲突时，严禁强行push，需处理好冲突后再push。
   2. push前请code review自己的改动，避免push时携带一些测试数据，而导致的上线问题。因为push后所引起的修改

基本遵循 [Semver](https://semver.org/lang/zh-CN/) 规范，并稍微做了点调整。

# Tag 规范

## 编写规范

### master分支tag规范

格式： major.minor.patch

如：1.0.0

### 子项目分支tag规范

格式：major.minor.patch-<项目名>[.<序号>]

如： 1.0.0-hsxc、1.0.0-hsxc.1

### 测试版本tag规范

格式：major.minor.patch-dev[.<序号>]

如： 1.0.0-dev、1.0.0-dev.1

### 业务项目规范

* major(主版本号): 当项目产生一个阶段性的升级时新增，
* minor(次版本号): 当项目做了新的功能或升级时新增,匹配`FEAT`、`CHORE`、`TEST`。
* patch(修订号): 当项目做了bug fix时新增，匹配`FIX`、`PERF`、`REFACTOR`、`REVERT`、`STYLE`。
  
### 工具库规范

* major(主版本号):当你做了不兼容的 API 修改，
* minor(次版本号):当你做了向下兼容的功能性新增，
* patch(修订号):当你做了向下兼容的问题修正。

## 使用说明

1. 标准的版本号只能基于master分支打版本

# push规范

   1. 原则上当出现push冲突时，严禁强行push，需处理好冲突后再push。
   2. push前请code review自己的改动，避免push时携带一些测试数据，而导致的上线问题。因为push后所引起的修改成本更高。

# 常用命令

*推荐使用rebase来进行管理操作,避免产生不必要的commit*

1. 当本地分支落后origin时，将本地新增提交推上master（本地：master, 目标origin/masters)

   ```bash
   # 同步本地origin与远程一致
   git fetch

   #基于开发分支rebase 最新的 master
   git rebase origin/master

   # 将更新后的commit提交
   git push
   ```

2. 删除某一条commit 记录

   ```bash
   git rebase -i head~10
   ```

   将光标移动到 待删除commit 前，通过 `dd` 快捷键 进行删除，然后 `esc > :wq`

3. 更换 commit 在 log 中的位置

   ```bash
   git rebase -i head~10
   ```

   复制目标commit到目标位置， 通过`dd` 快捷键 删除之前的 commit，然后 `esc > :wq`

4. 编辑log 中指定的commit

   ```bash
   git rebase -i head~10
   ```

   根据提示将目标commit 前的 `pick` 改为 `e`， 然后 `esc > :wq`，进如编辑状态

   修改代码后

   ```base
   git add .

   git rebase --continue
   ```
