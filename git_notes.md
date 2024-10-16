# Git Notes

[Git 官方网址](https://git-scm.com/) ：https://git-scm.com/



## 常用命令



在各种情况下常使用的Git命令：

- 工作区域

```bash
# 克隆
git clone
# 创建一个空的Git仓库或重新初始化现有仓库
git init
```

- 处理当前的更改

```bash
# 将文件内容添加到索引中
git add
# 移动或重命名文件、目录或符号链接
git mv
# 还原工作树文件
git restore
# 从工作树和索引中删除文件
git rm
```

- 检查历史和状态

```bash
# 使用二分查找引入错误的提交
git bisect
# 显示提交、提交和工作树等之间的变化
git diff
# 打印与图案匹配的线条
git grep
# 显示提交日志
git log
# 显示各种类型的对象
git show
# 显示工作树状态
git status
```

- 增长、标记和调整你的共同历史

```bash
# 下载部分克隆中缺失的对象
git backfill
# 列出、创建或删除分支
git branch
# 记录对存储库的更改
git commit
# 将两个或多个开发历史连接在一起
git merge
# 在另一个基础提示上重新应用提交
git rebase
# 将当前HEAD重置为指定状态
git reset
# 切换分支
git switch
# 创建、列出、删除或验证用GPG签名的标记对象
git tag
```

- 协作

```bash
# 从另一个存储库下载对象和引用
git fetch
# 从另一个存储库或本地分支获取并与之集成
git pull
# 更新远程仓库以及相关对象
git push
```

- 在本地全局设置个人信息:

```bash
git config --global user.name "终身学习"
git config --global user.email "5621268@qq.com"
```













|                             |                                         |      |
| --------------------------- | --------------------------------------- | ---- |
| `git --version` or `git -v` | 显示 Git 版本                           |      |
| `git init`                  | 创建一个空的Git仓库或重新初始化现有仓库 |      |
| `git clone`                 | 将存储库克隆到当前目录下                |      |
| `git add`                   | 将文件内容添加到索引中                  |      |
|                             |                                         |      |
|                             |                                         |      |
|                             |                                         |      |
|                             |                                         |      |
|                             |                                         |      |



## Github

### 本地新创建仓库

```bash
# HTTPS
echo "# stduy-notes" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/xjbieke/stduy-notes.git
git push -u origin main
# SSH
echo "# stduy-notes" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:xjbieke/stduy-notes.git
git push -u origin main
```

### 本地已有仓库

```bash
# HTTPS
git remote add origin https://github.com/xjbieke/stduy-notes.git
git branch -M main
git push -u origin main
# SSH
git remote add origin git@github.com:xjbieke/stduy-notes.git
git branch -M main
git push -u origin main
```







## Gitee

### 更改默认主分支名

**将Gitee已经存在的仓库中的默认主分支`master`改名为`main`**

本地仓库的操作

- 在本地仓库所在目录内使用`git branch -m`命令将本地的`master`分支重命名为`main`

```bash
git branch -m master main
```

- **推送更改到远程仓库**：

  使用`git push`命令将重命名后的分支推送到远程仓库，并设置`main`为新的默认分支。由于重命名分支会改变分支的引用，因此需要使用`-u`（或`--set-upstream`）选项来更新上游分支信息。可以先推送新分支，然后在Gitee上设置默认分支。由于只是推送一个重命名后的分支，并没有直接更改远程仓库的默认分支设置，所以通常不需要`--force`选项。只需确保远程仓库接受该分支的推送即可

  ```bash
  git push -u origin main
  ```

- 登录 Gitee 将默认分支改为 main分支 保存即可

> **注意事项**
>
> - 在执行这些操作之前，请确保你的本地仓库和远程仓库都是最新的，并且你已经提交了所有更改。
> - 如果你有其他协作者或团队成员在使用这个仓库，请在更改默认分支名称之前通知他们，以便他们能够相应地更新他们的本地仓库设置。
> - 更改默认分支名称后，可能需要更新你的工作流程、脚本或自动化工具以适应新的分支名称。
>
> 按照上述步骤操作后，Gitee仓库的默认主分支应该从`master`更改为`main`。









## Gitee 迁移仓库到 Github

- 在 Gitee 复制要迁移仓库的 HTTPS的链接地址
- 登录 Github 点击右上方➕，在下拉菜单中选择 `import repository`
- 在页面中 `The URL for your source repository` 的输入框填写 迁移仓库的 HTTPS的链接地址
- 在下面输入 gitee 的用户名和密码
- 最后输入导入的仓库的名字
- 点击 `Begin import` （开始导入）



## Git 同时绑定 Gitee 与 Github

==GIt 同时绑定 GItee 与 Github 进行 push 操作==

- 查看当前项目的远程仓库

```bash
# 显示读写远程仓库的名称和地址
$ git remote -v
origin  https://gitee.com/xjbieke/study-notes.git (fetch)
origin  https://gitee.com/xjbieke/study-notes.git (push)
# 当前指向仓库为 Gitee
```

- 将当前远程仓库重命名

```bash
# 修改远程仓库名称
$ git remote rename origin gitee
# 查看修改的结果
$ git remote -v
gitee   https://gitee.com/xjbieke/study-notes.git (fetch)
gitee   https://gitee.com/xjbieke/study-notes.git (push)
```

- 在 github 创建同名仓库，生成仓库链接地址

```bash
HTTPS: https://github.com/xjbieke/stduy-notes.git
SSH: git@github.com:xjbieke/stduy-notes.git
```

- 将新创建 github 远程仓库添加到本地

```bash
# 添加 github 远程仓库
$ git remote add github https://github.com/xjbieke/stduy-notes.git
# 查看修改的结果
$ git remote -v
gitee   https://gitee.com/xjbieke/study-notes.git (fetch)
gitee   https://gitee.com/xjbieke/study-notes.git (push)
github  https://github.com/xjbieke/stduy-notes.git (fetch)
github  https://github.com/xjbieke/stduy-notes.git (push)
```

- 我的仓库原来是gitee，默认分支名为：master，为了和github的默认分支名统一，将本地默认主分支名改为 main

```bash
$ git branch -m master main
```

- 推送更改到 gitee 远程仓库，先以新分支概念推送，

```bash
$ git push -u  gitee main
# 使用 -u 是由于重命名分支会改变分支的引用
```

- 登录 Gitee 在分支管理内将默认分支更改为 main 确认即可
- 向 github 仓库推送

```bash
```











