# Git版本控制器

## 参考文档
https://www.liaoxuefeng.com/wiki/896043488029600/

## git初始化
```js
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

## 创建版本库
1. git init 初始化仓库
2. git add filename  添加文件到仓库
3. git commit -m '注释'  提交文件到仓库

## 版本管理
### 状态命令
1. git status  查看仓库状态(是否有内容没有提交)
2. git diff    查看具体修改内容(如果add了就看不到了)
### 版本回退
1. git log  查看历史版本信息
2. git log --pretty=oneline  查看历史信息的简约版
3. git reset --hard HEAD^    回退版本(^个数代表回退的版本数量)
4. git reset --hard 版本号    直接到某个具体的版本中
5. git reflog  查看所有执行的版本信息
### 工作区、暂存区和版本库
- 工作区：正在开发的目录空间
- 暂存器：git add 将本地文件添加到暂存区
- 版本库：git commit  将暂存区的文件添加到版本库
### 管理修改
Git跟踪并管理的是修改，而非文件。
### 撤销修改
1. 工作区回退：git checkout -- filename
2. 暂存区回退：git reset HEAD filename(回到工作区) git checkout -- filename
3. 版本库回退：参考上述版本回退
### 删除文件
1. 本地删除:rm filename
    - 删除仓库文件：git rm filename(确定删除) git commit -m '提交'
    - 撤销删除文件：git checkout -- filename

## 分支管理
分支的概念：
    主分支：master，仓库自动生成的主分支
    子分支：独立创建的子分支
### 创建与合并分支
1. git checkout -b dev  创建并切换到分支
2. git branch           查看分支
3. git checkout 分支名称 切换分支
4. git merge dev        合并分支
5. git branch -d dev    删除分支
6. git branch 分支名称   创建分支
7. git switch 分支名称   切换分支

### 分支冲突解决
概念：版本管理是机械化，版本的合并只能基于一个版本进行合并
版本1 -> 版本2 -> 版本3
版本1 -> 版本3 // 错误
版本1：初始状态
版本2：dev();
版本3：devTools();
1. 冲突场景：把三个版本的内容全部保存下来，用户手动进行选择保留信息

### git忽略文件
.gitignore:写入到这里的文件和文件夹不会被git管理

## 远程仓库
### github
1. 第1步：创建SSH Key
    - 命令：ssh-keygen -t rsa -C "youremail@example.com"
2. 第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面
    - 登陆
    - 个人头像点settings
    - SSH and GPG keys
3. 第3步：复制id_rsa.pub放入到SSH keys中
    - 点击添加new SSH key
    - 将id_rsa.pub放入到key的输入框中，添加即可
4. 第4步：创建仓库
5. 第5步：生成token  Setting —— Developer setting —— 先选择个人访问令牌，再点击创建新令牌 —— 设置你的令牌 token的使用期限以及定义个人令牌的访问权限。—— token要复制下来保存好 —— 在密码位置直接填上上面你所生成的 token 密钥。
6. 第6步：上传到远程仓库
    - 将需要上传到远程仓库的项目提交到本地仓库
    - 关联远程仓库执行命令：git remote add origin https://github.com/xxxx/xxx.git
    - 上传到远程仓库：git push -u origin master(main换成主分支master)
    - 输入github的用户和密码
7. 第7步：关于markdown文件
    markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。
8. 第8步：修改文件，在次提交
    - git push

### gitee
1. 仓库地址：https://gitee.com/
2. 创建仓库
3. 克隆仓库
    - git clone url
4. 将需要放入到仓库的代码拷贝到克隆下来的本地仓库
5. 添加上传到本地仓库
6. 推送到远程仓库：
    - git push
7. 团队协作
    - 上传：git push
    - 下载：git pull
8. 冲突问题
    - 原因：多人同时操作同一个文件，都进行了上传操作
    - 解决：
        1. git pull更新一下
        2. 修改冲突部分的代码
        3. git add , git commit ,git push上传
        4. 通知和你冲突的人，更新一下：git pull