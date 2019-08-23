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

```python
import os

# Only works on Unix/Linux/Mac:
pid = os.fork()
print('Process (%s) start...' % os.getpid())
if pid == 0:
    print('I am child process (%s) and my parent is %s.' % (os.getpid(), os.getppid()))
else:
    print('I (%s) just created a child process (%s).' % (os.getpid(), pid))
```
运行结果：
```
Process (6382) start...
I (6382) just created a child process (6383).
Process (6383) start...
I am child process (6383) and my parent is 6382.
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

### c++ override说明符
现在假设这样一种场景，我们想要在派生类中定义一个函数，去覆盖基类中的虚函数，那么我们应该保证函数名以及形参列表都和基类中的一致，但由于粗心，把形参列表写得不一致了，这个时候跟我们的初衷就相违背了，派生类的函数没能够覆盖基类中的虚函数。但这种写法本身是合法的，编译器是不会报错的，想要调试和发现这种错误是很困难的。在c++11标准中，我们可以用override关键字说明派生类中的虚函数，这个时候，编译器将帮我们检测，若是使用了override关键字标记了的某个函数，这个函数没能覆盖已存在的虚函数，就会报错。
```c
struct B {
  virtual void f1(int) const;
  virtual void f2();
};

struct D : B {
  void f1(int) const override; //正确，f1与基类中的f1匹配
  void f2(int) override; //错误，B没有形如f2(int)的函数
}
```

### 流量控制 vs 拥塞控制
发送端要维护两个窗口：rwnd和cwnd，窗口字段的值的上限是它们的最小值
流量控制：点对点的流量控制，是接收端控制发送端，使得接收端的缓存来得及接收
拥塞控制：全局的过程，涉及所有主机和路由器，是由发送端自己通过检测网络状况决定的

#### 拥塞控制
发送方检测到超时：使用慢启动（指数）、拥塞避免（线性）
检测到3个冗余ACK：使用快速重传、快速恢复
流程：一开始慢启动，cwnd达到门限值的时候使用拥塞避免
1.当检测到超时，门限值变为当前cwnd的一半，cwnd设为1重新开始慢启动
2.当收到3个冗余ACK，立即重传丢失报文段，门限值变为当前cwnd的一半，cwnd变成这个新的门限值，开始拥塞避免算法

### 深信服远程面试（电话一面）
1.自我介绍
2.结构体内存对齐，为什么内存对齐，可变长结构体
3.strcpy有什么问题（我答的要小心内存覆盖的问题，自己实现的话要从后往前复制）
4.讲一下基数排序，堆排序
5.new和malloc的区别，是否可扩展（我答的ralloc），malloc最多分配多大的内存，又问了我对c++里面内存的理解（我答的 栈、堆、全局区）
6.hash表怎么实现的，冲突怎么解决
7.野指针（我回答的悬挂指针）
8.他从悬挂指针引申到 “对防御性编程有了解吗”（我说不太了解，应该是少写点bug吧，诸如不要写悬挂指针这类的）
9.extern关键字
10.问我平时怎么调试（我说主要是先定位问题的位置，再单步调试，查看变量和内存的状况），问了下linux命令知道哪些
11.算法题，从一篇英文文章里面找到单词出现次数数目前十的单词（我回答用hash map，遍历一遍存起来，再用一个数组a[10]保存次数最大的十个数，再遍历一遍，直接插入放进去），他问还有什么更好的方法吗（我说放进数组的时候也可以不用遍历一遍，利用快排的思想找map里面最大的10个数，可以降低到log(N)）
12.问了面试官，这次面试我的表现有什么可以改进的地方，他说简历里面项目还要再丰富一下，另外他们公司也在用容器，所以我二面的话要准备下容器方面的，还有数据库mongodb方面的

### 项目
#### 人脸识别
```
样本是单张人脸图像，所以靠样本来训练得到一个模型不太可行，这个时候可以换个思路，曲线救国，用一个训练好的人脸检测模型来对样本进行人脸检测，检测完之后再用关键点检测器对人脸的特征进行检测，把人脸的特征表达通过关键点检测以特征向量的形式存起来。在人脸识别系统中对测试图片进行同样的操作，把得到的特征向量和特征向量列表里的一一对比，最后返回欧氏距离最小的即为结果。
opencv人脸检测是基于haar特征的级联检测，优点是速度快，缺点是人脸稍微偏一点检测效果就不好；dlib人脸检测是基于HoG(方向梯度直方图)特征和SVM，相比opencv检测结果更准确，但速度也更慢。

为什么dlib比opencv慢？   我了解到的，dlib的计算量要比opencv的大很多。
```

#### Baas平台
```
各自都是一个完整的单页面应用  token都是保存在localstorage里
HMdashboard
后端：Python flask
前端：js react dva antdesign

运行流程：
首先运行起来服务端代码(设置监听端口，连接上mongodb数据库，将管理员用户名和密码存到数据库，注册flask蓝图)；
浏览器访问根路由，由flask控制的‘index路由’请求需要登录，这时跳到后端路由/login，然后返回一个前端模板文件index.html；
到了前端部分，前端根路由会根据一个权限的token决定是否渲染页面，第一次发过来的index.html中权限的token是为空的，所以前端路由跳到/user/login，输入用户名和密码之后，请求发送到后端；
后端根据用户名和密码查询数据库，若找到，则返回success和一个url，前端根据success和url进行跳转；
HMdashboard的功能分为创建主机和创建用户，创建主机时，指定类型(docker，k8s)、名字和ip等参数，后端接收到请求之后把host信息写到数据库表中，再对docker进行初始化(通过client = APIClient(base_url=worker_api, version="auto", timeout=timeout))，初始化包括指定daemon ip地址，创建两个bridge类型的网络(solo,kafka)，因为创建的容器在fabric中是以peer节点的形式存在，而且要保证他们之间的通信；
创建用户是指创建操作userdashboard的用户，把用户名和密码存到数据库表里；

初始化组织的时候，首先要根据userdashboard发来的配置信息，每个容器都要创建一个docker compose file，里面包含容器的启动以及配置信息(镜像路径、端口号、fabric配置文件挂载在本机的路径、容器内的环境变量等等)；创建容器的时候用到多线程
根据dockercompose file调用docker compose的python sdk把容器run起来(相当于docker-compose up)；
最后把创建容器的用户和组织写到数据库表；


userdashboard
后端：nodejs egg
前端：

运行流程：
首先通过egg-bin把服务端程序运行起来，浏览器中访问根路由，服务端返回一个index.tpl的模板文件；
由于还没做身份认证，代表权限的token为空，前端路由渲染/user/login页面；
填入用户名和密码，把它们发送到后端，这时用passport来做身份认证，具体的认证过程是，到数据库查询有没有跟这个用户名和密码相匹配的，认证成功后把浏览器路由重定向到根路由，同时把token发给前端；
userdashboard的功能目前有初始化组织和创建fabric网络，组织的初始化是指创建fabric网络中的peer节点、ca节点和orderer节点等等，初始化的请求要发送到hmdashboard；
创建fabric网络，首先读出数据库表中peer、oderer、org、ca节点的信息，然后设置fabric网络的相关配置文件的路径(包括key-value store，通道配置文件等等)，最后根据这些配置信息通过fabric node sdk还原一个fabric client对象；

借鉴了一些开源项目
难点：
一开始前端每次修改都要重新build，非常耗时，后来了解到可以使用mock使前端开发完全分离，每次修改完还可以自动build，不算难点，但在前期确实浪费了很多时间在上面；
在做登录模块的时候，一开始不知道怎么在浏览器客户端保存用户的登录状态，每次刷新就要重新登录，后来了解到可以用localstorage实现；
现在在进行创建通道的开发，通过fabric node sdk生成client，用client构建完请求之后发送给fabric网络，报错，还没解决；

亮点：
前后端分离做得很好，前端内容的改变不用重新加载整个页面，用户体验很好；
模板的渲染、路由的跳转也是在前端完成，后端简单地说只是用来处理请求；
第一次加载的体验也还好，因为前端静态文件不是放在一个文件里面，而是放在很多个文件里，分时发送到前端；
使用egg框架，把get和put方法都封装起来了，响应请求的时候只要调用router.get(),router.put()就行了，可以使开发专注与业务逻辑的实现；

```











