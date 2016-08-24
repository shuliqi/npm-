#前言

    nodejs的出现，可以算是前端里程碑式的一个事件，它让前端攻城狮们摆脱了浏览器的束缚，踏上了一个更加宽广的舞台。前端的可能性，从此更加具有想象空间。  随着一系列基于nodes的应用/工具的出现，工作中与nodejs打交道的机会越来越多。无论在node应用的开发，还是使用中，包管理都扮演着一个很重要的作用。NPM（node package manager），作为node的包管理工具，极大地便利了我们的开发工作，很有必要了解一下。

##一.npm是什么？

     npm就是随Node.Js一起安装的包管理器。所以说安装了node.js就已经安装了npm。
##二.npm的作用是什么？

     既然npm是Node.Js的包管理工具，所以肯定是用来管理node包。包括：安装包，更新包，查看包，卸载包，搜索包，发布包等。

    ###2.1  npm包安装


           
    包的安装有两种安装模式：本地安装，全局安装

 
     ####2.1.1  本地安装：package会被下载到当前所在目录，也只能在当前目录下使用 。例如在本地的一个localhost目录下：  


```javascript
   npm install        //npm install  jshint
```

    ####2.2.2   全局安装：package会被下载到到特定的系统目录下，安装的package能够在所有目录下使用。


```javascript
  npm install -g    //npm install -g jshint
```

    执行命令完毕后，将会创建一个node_modules目录(如果该目录不存在的话)，并下载安装的package到该目录。安装完成后，你会在node_modules目录下发现该package。

    注意：全局安装一个package时，可能会出现没有权限的错误提示，这表示对这个npm存储全局package和命令行工具的目录(npm安装目录)没有权限。解决的两种办法如下：
    ###（1）获取npm安装目录的权限
     
    #####a.查找 npm 全局包文件存储路径:

    在命令行敲如下命令：
    ```javascript
      npm config get prefix
    ```      
    #####b.获得npm安装目录权限:

    在命令行敲如下命令：
```javascript
     sudo chown -R  $(npm config get prefix)
```
    ###(2) 指定npm的默认安装目录为其他有权限操作的目录
        
    #####a. 创建一个用于安装全局package的目录:  
    
     mkdir glo
        b.配置NPM使用新的目录路径:
1
     npm config set prefix 'glo'
      
      c.打开或创建一个~/.profile文件，并添加这一行
 
1
     export PATH=~/glo/bin:$PATH

     d.回到命令行上，更新你的系统变量

1
     source ~/.profile
   
      2.2  package.json包安装
            
          每个项目的目录下面，一般都有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。npm install     命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。         
   
          下面是一个完整package.json文件
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
{
    "name": "welcom",
    "version": "0.0.1",
    "author": "舒丽琦",
    "description": "node.js程序",
    "keywords":["node.js","javascript"],
    "repository": {
        "type": "git",
        "url": "https://path/to/url"
    },
    "license":"MIT",
    "engines": {"node": "0.10.x"},
    "bugs":{"url":"http://path/to/bug","email":"bug@example.com"},
    "contributors":[{"name":"李四","email":"lisi@example.com"}],
    "scripts": {
        "start": "node index.js"
    },
    "dependencies": {
        "express": "latest",
        "mongoose": "~3.8.3",
        "handlebars-runtime": "~1.0.12",
        "express3-handlebars": "~0.5.0",
        "MD5": "~1.2.0"
    },
    "devDependencies": {
        "bower": "~1.2.8",
        "grunt": "~0.4.1",
        "grunt-contrib-concat": "~0.3.0",
        "grunt-contrib-jshint": "~0.7.2",
        "grunt-contrib-uglify": "~0.2.7",
        "grunt-contrib-clean": "~0.5.0",
        "browserify": "2.36.1",
        "grunt-browserify": "~1.3.0",
    }}
      2.1.1 认识package.json的属性

          属性很多，我就简单的介绍几个。

         2.1.1   name: package的名字

        2.1. 2   version: package的版本，当package发生变化时，version也应该跟着一起变化

        2.1.3    dependencies: package的应用依赖模块，即别人要使用这个package，至少需要安装哪些东东。应用依赖模块会安装到当前模块的node_modules目录下。

        2.1.4   devDependencies：package的开发依赖模块，即别人要在这个package上进行开发

        详细的可以戳这个：http://javascript.ruanyifeng.com/nodejs/packagejson.html

       2.3 npm包更新

      2.3.1  更新本地包：

       首先，在命令行工具(cmd)或者终端切换到项目目录package.json文件最好就放    在项目目录下。运行命令：

1
  npm update

      2.3.2  更新全局包：

      要更新某一个全局package包，可以使用npm install -g <package name>,例如：

1
  npm install -g jshint
     2.4 npm包卸载

      2.4.1  本地卸载包
     
       你可以从node_modules目录下卸载并删除一个package包，使用npm  uninstall <package name>命令，例如：

1
  npm uninstal jshint

      2.4.2 全局卸载包

      你可以从node_modules目录下卸载并删除一个全局package包，使用npm  uninstall －g  <package name>命令，例如：
1
  npm uninstall -g jshint

    2.5   npm包查看  

     2.5.1 查看本地包：在相应的目录下使用命令

1
  npm ls

    2.5.2  查看全局包：使用命令
1
  npm ls －g

    2.5.3  查看包的信息：使用命令

1
  npm ls <package name>

    2.6 npm包搜索  

1
 npm search <package name>    // npm search less
   
  三. 包的使用场景
 
   3.1 允许用户从npm服务器下载别人写好的包或者是命令行程序到本地来使用。
   3.2 允许用户提交自己写好的包或者命令行到命令行程序到npm服务器供别人下载使用。

  之前讲的知识点都是从npm服务器下载别人写好的包到本地来使用，那现在就讲如何讲如何发布自己的包到npm服务器


  3.3 例如：发布一个shuliqitest的package包到npm

（1）新建一个文件夹shuliqitest

（2）使用命令 npm init (创建一个package.json文件)

（3）在目录shuliqitest下面一个index.js文件
          
1
2
3
4
function hellowword(){
console.log("welcom shuliqi")
}
module.export= hellowword；

  (4)首先要注册一个npm账号(如果没有的话)----https://www.npmjs.com/

  (5) 注册完后，在命令窗口运行npm adduser(登陆npm),会提示你输入用户名和密码

  (6)登陆成功后，在shuliqitest目录下执行命令npm publish(发布package) 

  (7)布成功后就可以登陆到npm官网去看自己发布的package。https://www.npmjs.com/~shuliqi(我们刚才上传的)。

 3.4 更新自己发的包

    以发布的shuliqitest为例

 （1）改动shuliqitest目录下的index.js文件
   
1
2
3
4
function hellowword(){
console.log("welcom 哈哈哈哈")
}
module.export= hellowword；
（2）然后再命令行执行npm version patch, 此命令会把package.json的version更新


  (3)然后执行npm publish就可以更新到npm
           

   最后谢谢大家的阅读！！！1

