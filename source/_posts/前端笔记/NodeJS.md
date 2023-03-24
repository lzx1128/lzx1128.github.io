---
title: Nodejs基础教程
description: 🌮本文汇总Nodejs基础教程 ，可作为文档进行查询
mathjax: true
tags:
 - Nodejs
categories:
 - 前端笔记
abbrlink: 302
sticky: 2
cover: https://s1.vika.cn/space/2022/12/29/f9926ba0199241a6a1a3b2698e92ebc9
swiper_index: 2
date: 2023-03-20 18:19:03
updated: 2023-03-20 22:00:00
---


# Nodejs
## 介绍

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，是一个应用程序。

官方网址 <https://nodejs.org/en/>，中文站 <http://nodejs.cn/>

## 作用

- 解析运行 JS 代码 
- 操作系统资源，如内存、硬盘、网络

## 应用场景

* APP 接口服务
* 网页聊天室
* 动态网站, 个人博客, 论坛, 商城等
* 后端的Web服务，例如服务器端的请求（爬虫），代理请求（跨域）
* 前端项目打包(webpack, gulp)

## 使用

### 下载安装

工具一定要到官方下载，历史版本下载 <https://npm.taobao.org/mirrors/node/>

![img](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/20190329115938531.png?lastModify=1599473396)

Nodejs 的版本号奇数为开发版本，偶数为发布版本，<span style="color:red">我们选择偶数号的 LTS 版本（长期维护版本 long term service）</span>

![1572676490692](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/1572676490692.png?lastModify=1599473415)

双击打开安装文件，一路下一步即可😎，默认的安装路径是 `C:\Program Files\nodejs`

安装完成后，在 CMD 命令行窗口下运行 `node -v`，如显示版本号则证明安装成功，反之安装失败，重新安装。 

![1572678177784](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/1572678177784.png?lastModify=1599473424)

### 初体验

#### 交互模式

在命令行下输入命令 `node`，这时进入 nodejs 的交互模式

![1572678681282](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/1572678681282.png?lastModify=1599473439)

#### 文件执行

创建文件 hello.js ，并写入代码 console.log('hello world')，命令行运行 `node hello.js`

快速启动命令行的方法

* 在文件夹上方的路径中，直接输入 cmd 即可
* 使用 webstorm 和 vscode 自带的命令行窗口

![1572680753835](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/1572680753835.png?lastModify=1599473449)

#### VScode 插件运行

安装插件 『code Runner』, 文件右键 -> run code

![1593782861500](file://D:/project/git/h5200622-code/day09/%E8%AF%BE%E5%A0%82/1-NodeJS/%E8%AF%BE%E4%BB%B6/nodejs/assets/1593782861500.png?lastModify=1599473460)

#### 注意

<span style="color:red">在 nodejs 环境下，不能使用 BOM 和 DOM ，也没有全局对象 window和docu，全局对象的名字叫 global</span>



### Buffer(缓冲器)

#### 介绍

Buffer 是一个和数组类似的对象，不同是 Buffer 是专门用来保存二进制数据的

#### 特点

* 大小固定：在创建时就确定了，且无法调整
* 性能较好：直接对计算机的内存进行操作
* 每个元素大小为 1 字节（byte）

#### 操作

##### 创建 Buffer

* 直接创建 Buffer.alloc
* 不安全创建 Buffer.allocUnsafe
* 通过数组和字符串创建 Buffer.from

```js
// 创建一个长度为10字节的Buffer
let buf = Buffer.alloc(10);

let buf2 = Buffer.allocUnsafe(10);

let buf3 = Buffer.from("iloveyou");
```

##### Buffer 读取和写入

可以直接通过 `[]` 的方式对数据进行处理，可以使用 toString 方法将 Buffer 输出为字符串

* ==[ ]== 对 buffer 进行读取和设置
* ==toString== 将 Buffer 转化为字符串

```js
// Buffer内容的读取和设置
let res = buf3[1]; // 结果为10进制的数字
// 获取字符串形式
let res2 = buf3.toString();

// 设置内容
buf3[0] = 120;
```

##### 关于溢出

溢出的高位数据会舍弃

##### 关于中文

一个 UTF-8 的中文字符==大多数情况都是占 3 个字节==

##### 关于单位换算

1Bit 对应的是 1 个二进制位

8 Bit = 1 字节（Byte）

1024Byte = 1KB 

1024KB = 1MB

1024MB = 1GB

1024GB = 1TB

平时所说的网速 10M 20M 100M 这里指的是 Bit ，所以理论下载速度 除以 8 才是正常的理解的下载速度

### 文件系统 fs

fs 全称为 file system，是 NodeJS 中的内置模块，可以对计算机中的文件进行增删改查等操作。

##### 文件写入

* 简单写入
  * ==（引入模块）const fs = require("fs");==
  * fs.writeFile(filePath, data, [,options], callback);
  * fs.writeFileSync(file, data);
  * options 选项
    * `encoding` **默认值:** `'utf8'`
    * `mode`**默认值:** `0o666`
    * `flag` **默认值:** `'w'`
* 流式写入
  * fs.createWriteStream(path[, options])
    * path
    * options
      * ==flags==   **默认值:** `'w'`
      * `encoding `**默认值:** `'utf8'`
      * `mode`   **默认值:** `0o666`
    * 事件监听 open  close  eg:  ws.on('open', function(){});

##### 文件读取

* 简单读取
  * fs.readFile(file, function(err, data){})
  * fs.readFileSync(file)
  
* 流式读取
  
  * fs.createReadStream();
  
  ```js
  // 绑定事件
  const fs = require("fs");
  const rs = fs.createReadStream("index.html");
  // 绑定事件,data是确定好的，不能更改
  rs.on("data",(chunk)=>{
      console.log(chunk.toString());
  })
  // 关于小文件的读取-------readFile
  // 关于大文件的读取-------createReadStream
  ```
  
  
  
  ```js
  // 复制文件
  const fs = require("fs");
  const rs = fs.createReadStream("index.html");
  const ws = fs.createWriteStream("index-副本.html");
  
  // 第一种方法
  rs.on("data",chunk=>{
      ws.write(chunk);
  });
  // 第二种方法
  rs.pipe(ws);
  ```

##### 文件删除

* fs.unlink('./test.log', function(err){});

```js
// fs.unlink(路径,fun)
const fs = require("fs");
fs.unlink("bak.ini",err=>{
    if(err) throw err;
    console.log("删除文件");
});
```

* fs.unlinkSync('./move.txt');

##### 移动文件 + 重命名

* fs.rename('./1.log', '2.log', function(err){})

```js
// fs.rename(oldname,newname,fun);
// 改名命令只能执行一次，再次执行时会报错 （no such file or directory）
const fs = require("fs");
fs.rename("index,html","home.html",err=>{
  if(err) throw err;
  console.log("改名成功");
});

// 移动文件
fs.rename("index.html","./file/home.html",err=>{
    if(err) throw err;
    console.log("移动成功");
});
```

* fs.renameSync('1.log','2.log')

##### 文件夹操作

* mkdir  创建文件夹
  * path
  * options 
    * recursive 是否递归调用
    * mode  权限 默认为 0o777
  * callback 
* rmdir 删除文件夹
* readdir  读取文件夹

```js
// fs.mkdir(path,[,option],callback)
const fs = require("fs");
fs.mkdir("./project",err=>{
    if(err) throw err;
    console.log("创建文件夹成功");
})


// 删除文件夹,如果文件夹非空，使用recursive来一步清空
fs.rmdir("./project",{recursive:true},err=>{
     if(err) throw err;
    console.log("删除文件夹成功");
})

//读取文件夹
fs.readdir("d:/",(err,files)=>{
    if(err) throw err;
    console.log(files);
});
```

##### 关于路径

* 相对路径
  * ./index.html
  * ../images/logo.png
  * index.html
* 绝对路径
  * D:/www/share/day10/index.html (windows)
  * /home/root/index.html			

fs模块中，参数路径如果为**相对路径**的话，参照物是==执行命令时所在的工作目录==

__dirname 全局变量，始终保存的是==当前文件所在目录的绝对路径==

##### 查看文件的状态( fs.stat() )

```js
const fs = require("fs");
fs.stat(__dirname+"index.html",(err,stats)=>{
    if(err) throw err;
    console.log(stats);
   // 检查目标资源是否为文件夹
    console.log(stats.isDirectory());
   // 检查目标资源是否为文件
    console.log(stats.isFile());
});
```



## 附录

### unicode 字符集

* https://www.tamasoft.co.jp/en/general-info/unicode.html

* https://www.cnblogs.com/whiteyun/archive/2010/07/06/1772218.html    
