### Git和Github使用教程

**😈目录**

- 什么是git
- 使用git实现本地版本控制
- 连接git远程仓库
- git分支
- git和github

##### 1.什么是git

- 分布式

- 版本控制，如写论文的时候保留多个版本便于修改

  - 文件拷贝

  <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h017kvbe3aj20vq064dga.jpg" alt="image-20220217112346684" style="zoom:50%;" />

  - 本地文件管理：本机只保留一个文件（最新文件），其余文件通过工具存档

  - 集中式版本控制（SVN）

    <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h017kxmufcj20gm0bijro.jpg" alt="image-20220217112509760" style="zoom:50%;" />

  - 分布式版本控制

  <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h017kvpywdj20qi0fiwfr.jpg" alt="image-20220217113328363" style="zoom:50%;" />

- 软件

---

**补充：什么是SSH**

SSH是一种比较可靠的专为远程登录会话和其他网络服务提供安全性的协议，使用SSH协议可以有效防止远程管理过程中信息泄露的问题

---

##### 2.使用git实现本地版本控制

- `git init` 从头开始，在文件夹中创建 git 库，让git管理其文件夹

![image-20220220154307786](https://tva1.sinaimg.cn/large/e6c9d24egy1h017kx67mlj20ue02caaa.jpg)

![image-20220220154416746](https://tva1.sinaimg.cn/large/e6c9d24egy1h017kwnyofj20vq022weo.jpg)

- `git status`查看管理状态

![image-20220220154821374](https://tva1.sinaimg.cn/large/e6c9d24egy1h017kw77dwj20xs0aoq3u.jpg)

- 执行 `git add <filename> `将文件纳入管理，filename 支持通配符，最常用的就是点(.)表示所有文件

  再次执行 git status，则显示有待提交（to be committed），此时文件已经开始被 git 管理了，文件进入一种暂存状态（stage），如果想反悔可以用` git rm --cached` 使其进入 unstage 状态

- 执行 `git commit` 将文件的变更从暂存区提交入库。

![3 area](https://doc.shiyanlou.com/courses/3083/1505711/26e18cfe9763e915d2057925ee7a1a23-1)

`git add` 并不需要你填写说明（log），也不需要记录你的用户信息（name、email），相当于你完成了每份作业，随手扔到书包里，允许你随时拿出来修改，修改完再扔到书包里 —— 这个过程不做任何限制。但 `git commit` 就像你把作业要交给老师了，必须要在作业上填写自己的姓名、班级，甚至给老师写个 log，比如：“我昨晚练钢琴了，很晚才写数学，当时已昏昏欲睡”，提醒老师数学错题多不要怪我。

- 回滚版本`git reset --hard (log对应编号)`

三个区域：

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9805timestamp1548755776759.png)

##### 3.连接git远程仓库

git 能够与使本地库和远程库保持一种同根同源，但又若即若离的关系，git 不讲求集中式管理，没有一个必然的中心节点，每一个终端上的版本库都是一份完整的历史，可以随时与多个远程库互联和同步，**每一个远程库与本地库地位平等，随时可以同步，也随时可以分裂。**

- git版本库的分发
  - 本地：类似拷贝粘贴（`git clone <origin.repo> <local.repo>` ）
  - ssh从远程clone版本库：`git clone <user>@<host>:<path> [-p port]`

- `git pull`

  更新了远程库的代码后，在本地使用`git pull`获取最新版本

- git远程URL

  - 从别处 clone 来的版本库，相比本地 `git init` 的库，具有了一个 remote 的属性，用来记录该版本库的远程 URL 在哪里，使用 `git remote -v` 来查看

  - 一个 git 版本库可以有多个 remote，每个 remote 就像它的一个根，版本库可以从多个 remote 拉取代码，也可以向任何一个 remote 推送代码，就像这个 Github 的标志动物：<img src="https://doc.shiyanlou.com/courses/3083/1505711/90c58883bfbdc4ef16706a1420504264-0" alt="github octocat" style="zoom:25%;" />

  - 添加多个remote：`git remote add <name> <url>`

    ```bash
    $ cd hello-world/
    $ git remote add oneremote # 添加新的远程库
    $ git remote -v # 查看远程库信息
    $ git pull oneremote # 拉取指定remote的更新信息
    ```

- 裸版本库

  **分享：作为协作开发的中心点！** —— 将一个裸版本库放在 Server 上，开发团队的成员们从 Server 上 clone、pull、push 代码。

  得到一个裸版本库有几种办法：

  1. `git init --bare ...`：直接从零创建一个裸版本库，它是没有 remote 的。
  2. `git clone --bare ...`：从远程 clone 一个库到本地，但存储为裸库，无法 checkout 出工作文件，但它是有 remote 的
  3. `git push` 能够将本地的修改推送到 remote 上，但要求 remote 必须是裸版本库。

- git 裸版本库还为 git 的裂变提供在最方便的手段：`git clone --bare` 得到他人的一个版本库的裸库，然后把自己的 ip（或域名）发布出去，接受用户 push 的提交，后续就可以与原来的版本库分道扬镳，独自演进。这种快速裂变的方式让项目最初的作者无法控制项目的走向，没有中央集中式的管控手段，所以最好的办法就是：项目建立的第一次提交就写好 License 和必要的声明，然后保持一个开放的心态，假如他人裂变出去的项目发展的更好，要欣然接受，互联网会记住一切。

  这种项目裂变，后来被 github 简化成了 fork 操作

##### 4.git分支

![功能分支工作流· Git 指南](https://carney520.gitbooks.io/git-guide/content/branch/images/feature_flow.png)

![git.diff.svg](https://doc.shiyanlou.com/courses/3083/1505711/785632cea774450fa2c6e6c79c354fc9-1)

- `git diff`：已修改，但尚未缓存（即：没有 `git add`）的文件与索引区文件比较差异
- `git diff --cached`：已经缓存，但尚未提交（即：没有 `git commit`）的文件差异
- `git diff <ref.id>`：当前未提交（即上述两种情况的合集）与指定版本`<ref.id>`之间的差异，其中 ref.id 可以是
  - 某次提交的 hash 值，如：`git diff 6eff`
  - `HEAD`：未提交与版本库里最新版本之间对比差异
  - `HEAD^`：与 HEAD 的前一个版本之间对比差异
- `git diff <ref.id1> <ref.id2>`：两个版本之间的差异
- 查看分支`git branch`
- 新建分支`git branch <name>`
- 转换分支`git checkout <name>`
- 合并分支`git merge <name>`（注意切换分支）
- 删除分支`git branch -d <name>`

<img src="https://doc.shiyanlou.com/courses/3083/1505711/384d879ccd3319ca8e7fe91628fff393-1" alt="git.branch.svg" style="zoom:50%;" />



##### 5.git和github

---



