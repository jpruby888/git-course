# git

## 一、配置
1. 配置用户名和邮箱：
   - 使用以下命令进行配置。
   ```bash
   C:\\Users\\jpruby
   git config --global user.name "jpruby"
   C:\\Users\\jpruby
   git config --global user.email "japan8364@163.com"
   ```

## 二、使用 git
1. `git status`：查看仓库当前状态。
   ```bash
   C:\\Users\\jpruby\\Desktop\\vue-course\\git-demo
   git status
   fatal: not a git repository (or any of the parent directories):.git
   ```
2. `git init`：初始化仓库。
   ```bash
   C:\\Users\\jpruby\\Desktop\\vue-course\\git-demo
   git init
   Initialized empty Git repository in C:/Users/jpruby/Desktop/vue-course/git-demo/.git/
   ```
3. 文件状态转换：
   - 未跟踪状态转换为暂存状态：
     - `git add <filename>`：将指定文件切换到暂存状态。
     - `git add.`：提交所有未跟踪的内容。
   - 暂存状态转换为未修改状态：
     - `git commit -m "message you want to note"`。
     - `git commit -a -m "xxxx"`：提交已修改的文件（未跟踪的文件不会提交）。

## 三、常用命令
1. 重置文件：
   - `git restore <filename>`：恢复文件。
   - `git restore *`。
   - `git restore --staged filename`：取消暂存状态。
2. 删除文件：
   - `git rm filename`：删除文件。
   - `git rm filename -f`：强制删除。
3. 移动文件：
   - `git mv from to`：移动文件或重命名文件。

## 四、分支
1. 分支结构：
   - Git 存储文件时，每一次代码提交都会创建与之对应的节点，这些节点构成树状结构。默认情况下仓库中只有一个名为 `master` 的分支，在使用 Git 时，可以创建多个分支，分支之间相互独立，在一个分支上修改代码不会影响其他分支。
   - 分支结构示意图：
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89c57cdf-757d-4828-8f4b-461284a36937/c9d9f862-01b2-450c-9018-b128ac938790/image.png)
2. 分支操作：
   - 查看分支：`git branch`。
   - 创建分支：`git branch <branch name>`。
   - 删除分支：`git branch -d <branch name>`。
   - 切换分支：`git switch <branch name>`。
   - 创建并切换分支：`git switch -c <branch name>`。
   - 开发中通常在自己的分支上编写代码，完成后将分支合并到主分支。

### （一）变基（rebase）
1. 与 `merge` 的对比：
   - 当项目复杂、开发过程波折时，反复创建、合并、删除分支会使代码提交记录混乱，而变基可以使提交历史更加线性和清晰。
2. 变基过程：
   - 找到两条分支的最近共同祖先。
   - 对比当前分支相对于祖先的历史提交的不同，并存储到临时文件中。
   - 将当前分支指向目标分支的最新提交。
   - 重放特性分支的修改。
   - 变基原理图：
   ```mermaid
   graph TD;
       A[共同祖先] --> B[主分支];
       A --> C[特性分支];
       B --> D[主分支新提交];
       C --> E[特性分支新提交];
       E -.变基.-> F[主分支最新提交];
       F --> G[特性分支重放];
   ```
   - 变基过程说明：
     - 找到共同祖先：图中的 A 节点。
     - 提取特性分支的修改：C 到 E 的变化。
     - 将特性分支指向主分支最新提交：E 指向 F。
     - 重放特性分支的修改：在 F 之后应用特性分支的修改，形成 G。