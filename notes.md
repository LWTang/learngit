### git步骤

* 远端建仓库
* 本地写代码、本地add、commit
* push到远端（远端有readme.md的时候要先用 git pull --rebase origin master 来合并）

### git删除远程库文件

1. git rm filename
2. commit
3. push

### debug
* github上显示表格的时候要在表格前面空一行
* 在github push项目出错，原因是在github.com改了之后没有merge，要先pull，再push，成功解决

### git远程和本地同步

1. 远程建仓库，本地建仓库,本地初始化：```git init```
2. (在新的电脑上: `ssh-keygen -t rsa -C "1770723422@qq.com"`在用户主目录生成公钥和私钥，将公钥添加到账户的ssh key；设置提交的信息```git config --global user.email 1770723422@qq.com```和```git config --global user.name LWTang```)
3. 将远程和本地库关联起来：```git remote add origin git@github.com:LWTang/PyQt-learn.git```
4. 将远程库pull到本地：```git pull origin master```
5. 开始表演(⊙o⊙)…

### 在仓库显示图片
```js
https://github.com/LWTang/项目名/raw/master/图片在仓库的路径
```