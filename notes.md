### git步骤

* 远端建仓库
* 本地写代码、本地add、commit
* push到远端（远端有readme.md的时候要先用 git pull --rebase origin master 来合并）

### git删除远程库文件
rm 实际是从暂存区移除
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
```
![](https://github.com/LWTang/项目名/raw/master/图片在仓库的路径)
```

### git clone
```
git clone git://github.com/schacon/grit.git mygrit
```
这样目录名为 mygrit 而不是 grit

### .gitignore文件
```
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a
# 但 lib.a 除外
!lib.a
# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO
# 忽略 build/ 目录下的所有文件
build/
# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
# 忽略 doc/ 目录下所有扩展名为 txt 的文件
doc/**/*.txt
```

### git status
列出修改过的文件

### git diff
查看具体修改了什么

### git mv
```
git mv file_from file_to
```
用来移动文件，也可以用来重命名

### 取消已暂存的文件
```
git reset HEAD test.txt
```

### 撤销最后一次提交
```
git commit --amend
```

### 多进程
#### fork()系统调用
fork()调用一次，返回两次，分别在子进程和父进程里返回，在子进程里返回0，在父进程里返回子进程的id。因为父进程要通过fork拿到子进程的id，而在子进程里可以通过getppid()拿到父进程的id
```python
import os

print('Process (%s) start...' % os.getpid())
# Only works on Unix/Linux/Mac:
pid = os.fork()
if pid == 0:
    print('I am child process (%s) and my parent is %s.' % (os.getpid(), os.getppid()))
else:
    print('I (%s) just created a child process (%s).' % (os.getpid(), pid))
```
运行结果：
```
Process (876) start...
I (876) just created a child process (877).
I am child process (877) and my parent is 876.
```

### js(...)
1. 展开语法：
将数组或者对象展开
```js
//数组展开
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1 = [...arr2, ...arr1]; // arr1 现在为 [3, 4, 5, 0, 1, 2]

//对象展开
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 }; // 克隆后的对象: { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 }; // 合并后的对象: { foo: "baz", x: 42, y: 13 }
```

2. 剩余参数
将一个不定数量的参数表示为一个数组
```js
function multiply(multiplier, ...theArgs) {
  return theArgs.map(function (element) {
    return multiplier * element;
  });
}

var arr = multiply(2, 1, 2, 3); 
console.log(arr);  // [2, 4, 6]
```
