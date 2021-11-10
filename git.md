# Git使用规范

### 前言

1. 企业采用 github 进行代码托管，所有项目源码均存放于github上
2. 企业采用Github Flow工作流进行代码管理
3. 企业 github 地址 <https://github.com/mockingbot>
4. 当需要指定仓库权限时，请联系github管理员（长熙）

# Github Flow

1. 根据需求，从`master`拉出新分支，不区分功能分支或补丁分支。
2. 在本地分支完成功能开发后，提交代码，并及时推送至远程仓库。
3. 当想合并分支时，可以发起一个 pull request（简称PR）。
4. 当 review 或者讨论通过后，你的pull request被接受，代码会合并到目标分支。
5. 一旦合并到 master 分支，及时部署。

说明：

* 只有一个长期分支 master ,而且 master 分支上的代码，永远是可发布状态,一般 master 会设置 protected 分支保护，只有有权限的人才能推送代码到 master 分支。
* 本企业除imock-rails仓库以edge分支作为主分支，其他均以master分支作为主分支。

* pull request既是一个通知，让别人注意到你的请求，又是一种对话机制，大家一起评审和讨论你的代码。`对话过程中，你还可以不断提交代码`。

### 使用流程

1. 根据项目需求从github上拉取代码仓库

   ```bash
   git clone <仓库地址>
   ```

2. 根据任务目标在github上新建目标分支，如：yj/ws，并拉取到本地，作为修改代码仓库

   ```bash
   git fetch  #github上新建分支后执行，在本地获取仓库的变更记录，此处获取新建的分支记录
   git checkout <分支名> #在本地建立分支，与origin上分支名保持一致
   ```

   注意：分支名请根据Branch规范进行合理命名，方便识别及管理

3. 修改代码后，提交修改内容

   ```bash
   git add <修改内容> #提交代码到暂存区
   git commit  -m '[description]'  #添加commit描述
   git push #将本地commit push到github上
   ```

   注意：

   * commit 描述需按照commit规范进行添加
   * 原则上每完成一个功能需要提交一个commit
   * push代码时，若遇到冲突，禁止强行push，需在本地解决冲突后再push（自己个人分支确认后除外）

### Branch规范

##### 使用规范

1. 每当开始一个新的任务时，需要从目标仓库切一个branch出来，作为自己的工作空间
2. 根据需求从目标branch切出自己的branch，一般是从master或edge 切出
3. 分支命名需以英文命名，如无必要，禁止使用拼音
4. 当描述需要多个单词，以中划线（-）进行连接，如  yj/update-mb-rich-text

##### 命名规范

1. 分支项目命名规范

   格式：<姓名简称>/<项目名称或简称>[-<目的>]

   参考：yj/ws、yj/ws-rebase

2. 主项目命名规范

   格式：<姓名简称>/<功能目的>

   参考：yj/theme、yj/update-mb-rich-text

3. 生产/开发分支命名规范

   格式：（prod|dev）/<项目名称>

   参考：prod/ws、dev/ws

4. 特殊分支命名规范

   主分支：master

   内测环境：edge

### commit规范

##### 前言

1. 公司采用rebase 机制来进行commit管理，这样保证了代码commit的整洁干净。

##### 编写规范

1. commit文本规范

   格式：<type>: description

   注意：冒号后有一个空格

   type类型：

   ADD: 添加一个新功能

   FIX: 修复一个功能

   DEL: 删除一个功能或一个文件
   UPG: 更新一个仓库版本
   OPT: 优化

   DOC: 文档修改
   TEST: 测试版本

   STYLE: 优化样式

   CI： 与CI（持续集成服务）有关的改动

   REF:  代码重构

   description推荐为中文，必要关键字或表达需要情况下使用英文

2. commit提交规范

   原则上是处理一个issue，提交一个commit,若同时处理了多个问题，需要将commit拆成多个来提交

# push规范

   1. 原则上当出现push冲突时，严禁强行push，需处理好冲突后再push。
   2. push前请code review自己的改动，避免push时携带一些测试数据，而导致的上线问题。因为push后所引起的修改

   Tag 规范

# 常用Git命令
