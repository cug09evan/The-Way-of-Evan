# 目的

在GitHub上记录学习过程，保证一周产出一篇文章

# 命令操作

1. git init 将某个目录初始化为git目录，包含隐藏文件.git

2. 设置签名：区分不同开发人员的身份---用户名和email地址

   1. 设置的签名和登录远程库的账号密码没有任何关系
   2. 命令：git config
      1. 项目级别/仓库级别：仅在当前本地库有效  
         1. git config user.name evan
         2. git config user.email cug09evan@163.com
         3. 信息保存的位置是：当前目录.git下的config文件中
      2. 系统用户级别：登录当前操作系统的用户范围
         1. git config --global  user.name evan
         2. git config --global  user.email cug09evan@163.com
         3. 信息保存位置：cat ~/.gitconfig文件中
      3. 级别优先级原则：项目级别优于系统级别
      4. 二者都没有，是不允许的

3. git status： 查看工作区和暂存区状态

4. 一个文件在git管理中所使用的命令

   1. vim readme.txt：目录下创建文件
   2. git add readme.txt: 将readme.txt文件从工作区添加到 暂存区
   3. git rm --cached readme.txt：将readme.txt文件从暂存区中删除，本地该文件还是存在
   4. git commit -m "DEV：指南" readme.txt：将readme.txt文件推到本地库上

5. git log:查看git提交日志

   1. git log --pretty=oneline:历史记录只展示一行
   2. git log --oneline: hash值只显示部分,只能显示当前分支及该分支之前的历史记录
   3. git reflog: 移动到当前版本需要的步数,可显示所有的操作记录

6. 前进/后退历史版本

   1. 基于索引值操作（推荐）
      1. git reset --hard [局部索引值]
      2. 例子：git reset --hard  ce2101a
   2. 使用^符号:只能后退
      1. git reset --hard HEAD^^
      2. 解释：一个^表示后退一步，两个表示后退两步
   3. 使用~符号：只能后退
      1. git reset --hard HEAD~2    后退两步
   4. reset命令三个参数对比
      1. --soft：仅仅在本地库移动HEAD指针
      2. --mixed：
         1. 在本地库移动HEAD指针
         2. 重置暂存区
      3. --hard：
         1. 在本地库移动HEAD指针
         2. 重置暂存区
         3. 重置工作区
   5. 删除文件并找回
      1. 前提：删除前，文件存在时的状态提交到本地库
      2. 操作： git reset --hard [指针位置]
         1. 删除操作已经提交到本地库，指针位置指向该文件存在时的版本hash值
         2. 删除操作未提交到本地库，指针位置指向当前版本 HEAD
   6. 比较文件差异
      1. git diff [文件名]
         1. 将工作区中的文件和暂存区进行比较
      2. git diff [本地库中历史版本] [文件名]
         1. 将工作区中的文件和本地库历史记录比较
      3. 不带文件名比较多多个文件

   ## 分支管理

   1. 查看当前分支状况：git branch -v

   2. 创建新分支：git branch [分支名称]

   3. 检出分支：git checkout [分支名称]

   4. 合并分支：

      1. 第一步：切换到接受修改的分支（被合并，增加新内容）
         1. git checkout [被合并分支名]
      2. 第二步：执行 git merge [有新内容分支名]

   5. 解决冲突

      1. 冲突的表现
      2. 冲突的解决
         1. 第一步：编辑文件，删除特殊符号
         2. 第二步：将文件修改到满意的程度，保存退出
         3. 第三步：git add [文件名]
         4. 第四步：git commit -m "日志信息"
            1. 注意：此时commit一定不能带文件名

   6. 本地库与远程库交互

      1. git remote -v ：查看是否有远程库地址对应的别名
      2. git remote add [别名] [远程库地址]
         1. git remote origin https://.....
      3. git push [远程库别名] [本地分支名称]
         1. git push origin master

   7. 克隆：git clone []

      1. 完整的把远程库下载到本地
      2. 创建origin远程地址别名
      3. 初始化本地库

   8. 拉取：pull = fetch + merge

      1. git fetch [远程库地址别名] [远程分支名]
      2. git merge  [远程库地址别名/远程分支名]
      3. git pull [远程库地址别名] [远程分支名]

   9. 忽略特定文件

      1. 在~/.gitconfig文件中引入文件名

         ```
         [core]
         	excludesfile=C:/Users/Lenove/java.gitignore
         
         文件内容从：https://github.com/github/gitignore/blob/master/Java.gitignore 获取并添加
         .classpath
         .project
         .settings
         target
         ```

         


