## Bash的基本指令

1. pwd  查看当前所在目录
2. cd /etc/  进入一个目录

3. mkdir /etc/  建立新目录

4. gedit /etc/  编写C的源代码

5. touch file  创建一个名为file的文件

6. ls  显示目前目录的所有文件

7. ls *.txt  查找txt文件

8. *匹配0或多个字符
9. ?  匹配任意一个字符cd

10. 可用tab键补全相关命令

11. ctrl+a  将光标移至开头

12. ctrl+e  将光标移至行末
13. clear  清屏
14. rm  删除
15. rm -rf  删除一个文件夹
16. mv  /被移动文件/ /想要移进的文件夹/
17. reset  重新初始化终端
18. history  查看历史命令
19. help  帮助
20. exit  退出
21. cd .. 回到上一级文件
22. tar -zxvf /etc/   解压
23. sync 将数据由内存保存到磁盘中
24. shutdown -h now 立马关机
25. reboot 重启
26. vim /etc/ 用vim编辑器打开文件进行编辑

可用键盘上键恢复之前输入过的命令

## Vim编辑器

三种模式

- 命令模式 command mode
- 输入模式 insert mode
- 底线命令模式

以下常用命令

- **i** 切换到输入模式，以此来输入字符
- **x** 删除当前光标所在处的字符
- **：**切换到底线命令模式，以在最底一行输入命令。（需要先退出编辑模式）
- ESC 退出到命令模式

**底线命令模式**

在命令模式系下按:就进入了底线命令模式。光标移至最底下，此时就可以输入一些底线命令了！



-------

```bash
# 设置名称与标识
git config --global user.name Yutsing #名称
git config --global user.email 630853319@qq.com #邮箱
```

Git Bash：Unix与Linux风格的命令行

Git CMD：Windows风格的命令行

Git GUI：图形化界面，不好用

## Git的理论核心

- Workplace：工作区，平时存放项目代码的地方
- Index/Stage：暂存区，用于临时存放改动，保存即将提交到文件列表的信息
- Repository：仓库区，即安全存放数据的位置，里面有提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可认为是项目组中的一台电脑用于远程的数据交换

## Git的工作流程

1. 在工作目录中添加、修改文件
2. 将需要进行版本管理的文件放入暂存区域
3. 将暂存区域的文件提交到Git仓库

Git管理的三种状态：modified，staged，committed

## Git项目的搭建

### 本地仓库搭建

```bash
# 在当前目录创建一个git代码库
git init
```

### 克隆远程仓库

```bash
# 克隆一个项目和它的整个代码历史
git clone [url]
```

## Git文件操作

文件四种状态

- untracked：未跟踪，此文件在文件夹中，但并没有加入到git库，不参与版本控制。通过**git add** 变为staged
- unmodify：
- modified：
- staged：

```bash
#查看文件状态
git status [filename]

#查看所有文件状态
git status

# git add . 添加所有文件到暂存区
# git commit -m '信息' 提交暂存区中的内容到本地仓库 -m 提交信息
```

### 忽略文件

在主目录下建立”gitignore’文件

```bash
*.txt #忽略所有  .txt结尾的文件
!lib.txt #lib.txt除外
/temp #仅忽略项目根目录下的TODO文件，不包括temp
build/ #忽略build/目录下的所有文件
doc/*.txt #会忽略doc/notes.txt 但不包括doc/server/arch.txt
```

