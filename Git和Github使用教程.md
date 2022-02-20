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

  <img src="/Users/anita/Library/Application Support/typora-user-images/image-20220217112346684.png" alt="image-20220217112346684" style="zoom:50%;" />

  - 本地文件管理：本机只保留一个文件（最新文件），其余文件通过工具存档

  - 集中式版本控制（SVN）

    <img src="/Users/anita/Library/Application Support/typora-user-images/image-20220217112509760.png" alt="image-20220217112509760" style="zoom:50%;" />

  - 分布式版本控制

  <img src="/Users/anita/Library/Application Support/typora-user-images/image-20220217113328363.png" alt="image-20220217113328363" style="zoom:50%;" />

- 软件

---

**补充：什么是SSH**

SSH是一种比较可靠的专为远程登录会话和其他网络服务提供安全性的协议，使用SSH协议可以有效防止远程管理过程中信息泄露的问题

---

##### 2.使用git实现本地版本控制

- `git init` 从头开始，在文件夹中创建 git 库，让git管理其文件夹

![image-20220220154307786](/Users/anita/Library/Application Support/typora-user-images/image-20220220154307786.png)

![image-20220220154416746](/Users/anita/Library/Application Support/typora-user-images/image-20220220154416746.png)

- `git status`查看管理状态

![image-20220220154821374](/Users/anita/Library/Application Support/typora-user-images/image-20220220154821374.png)

- 执行 `git add <filename> `将文件纳入管理，filename 支持通配符，最常用的就是点(.)表示所有文件

  再次执行 git status，则显示有待提交（to be committed），此时文件已经开始被 git 管理了，文件进入一种暂存状态（stage），如果想反悔可以用` git rm --cached` 使其进入 unstage 状态

- 执行 `git commit` 将文件的变更从暂存区提交入库。

![3 area](https://doc.shiyanlou.com/courses/3083/1505711/26e18cfe9763e915d2057925ee7a1a23-1)

`git add` 并不需要你填写说明（log），也不需要记录你的用户信息（name、email），相当于你完成了每份作业，随手扔到书包里，允许你随时拿出来修改，修改完再扔到书包里 —— 这个过程不做任何限制。但 `git commit` 就像你把作业要交给老师了，必须要在作业上填写自己的姓名、班级，甚至给老师写个 log，比如：“我昨晚练钢琴了，很晚才写数学，当时已昏昏欲睡”，提醒老师数学错题多不要怪我。

- 回滚版本`git reset --hard (log对应编号)`

三个区域：

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9805timestamp1548755776759.png)

##### 3.连接git远程仓库

`git clone <origin.repo> <local.repo>` 如果 `<local.repo>` 省略不写，则创建 `<origin.repo>` 的同名文件夹。clone 后，继续和 Server 上的版本保持更新，则可以使用 `git pull` 或 `git fetch` 命令，我们先演示 pull 拉取。

- 首先在origin.repo中做一些更新，并提交

- 然后进入 local.repo ，进行 `git pull` 操作拉取在 origin.repo 中的更新

##### 4.git分支

![功能分支工作流· Git 指南](https://carney520.gitbooks.io/git-guide/content/branch/images/feature_flow.png)

![git.diff.svg](https://doc.shiyanlou.com/courses/3083/1505711/785632cea774450fa2c6e6c79c354fc9-1)

- 查看分支`git branch`
- 新建分支`git branch <name>`
- 转换分支`git checkout <name>`
- 合并分支`git merge <name>`（注意切换分支）
- 删除分支`git branch -d <name>`

##### 5.git和github

---

#### 使用git实现本地版本控制

利用 Github Pages 的特性来部署由 Hexo 框架渲染生成的静态博客，并且为博客添加插件以实现个性化博客、评论、七牛实现图床等功能。

