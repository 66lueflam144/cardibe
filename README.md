# Start with Docs

> The first project（feat windows 11）.



## step 0
检查本地有没有Node.js<br>:arrow_right:直接在所有应用中搜索Node.js即可<br>还要检查一下环境变量里PATH是否有其路径。
<a href="https://www.runoob.com/nodejs/nodejs-tutorial.html"><br>了解Node.js请往这来</a>

## step 1 下载docsify
有了Node.js后，可以在powersell输入<br>
```Bash
npm i docsify-cli -g
```
以此来下载docsify。

## step 2 创建项目

初始化创建项目的命令:arrow_down:
```Bash
docsify init ./projectname
```
- `projectname`是自己给项目的名字。
- 如果想在其他目录下创建项目，就在该目录下或者进入该目录打开PowerShell执行上方命令进行创建以及初始化项目。
  
>不过在windows系统上默认禁止运行脚本，第一次初始化项目会提示`禁止`错误。<br>解决方法如下，如果看详情[原文](https://blog.csdn.net/m0_60698858/article/details/123664109)在这里。
```Bash
//以管理员身份打开windows powershell，输入
Get-ExecutionPOlicy -list
//可以得到一个Scope&ExecutionPolicyb表单，基本在ExecutionPolicy那一列都是Undefined的值——有效的执行策略是RemoteSigned，当前用户的执行策略优先于为本地计算机设置的策略。
//我们需要更改设置执行策略
set-ececutionpolicy remotesigned
//然后会出现选项，输入y再回车即可。
```

### 基础配置文件

|文件|作用|
|---|---|
|index.html|基础配置项（入口文件）|
|README.md|主业内容渲染文件|
|<font color=pink>_coverpage.md</font>|封面配置文件|
|<font color=pink>_sidebar.md</font>|侧边栏配置文件|
|<font color=pink>_navbar.md</font>|导航栏配置文件|
|<font color=pink>favicon.ico</font>|浏览器图标|

>粉色字体的文件需要自己添加，原项目初始化文件夹中没有。

>在README.md中使用markdown语法写内容即可完成对blog内容的编辑修改。

:smile:如果想启用封面，侧边栏，导航栏，浏览器:arrow_down:

### 对基础配置项编辑

```html
<!--index.html-->
<head>
    <!--设置浏览器图标-->
    <link rel="icon" href="/favicon.ico" type="image/x-icon" />
    <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon" />
    <!--设置主题,href里面的内容可更改来更改主题-->
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/theme/vue.css">
</head>

<body>
    <!--定义加载时的动作-->
    <div id="app">加载中...</div>
    <script>
        windoe.$docsify={
            name:'',//项目名字
            repo:'',//Github仓库地址
            //以下需要手动输入配置
            loadSidebar:true,//侧边栏支持，，默认加载是项目根目录下的_sidebar.md文件
            loadNavbar:true,//导航栏支持，，默认加载是项目根目录下的_navbar.md文件
            coverpage:true,//封面支持，，默认加载是项目根目录下的_coverpage.md文件
            maxLevel:num,//最大支持渲染的标题层级，num为可修改数字
            subMaxLevel:num,//设置生成目录的最大层级（建议2-4）
            mergeNavbar:true,//小屏设备下合并导航栏与侧边栏
        }
    </script>
```
to be continue...

### coverpage
（前提是在`index.html`文件中设置打开了渲染封面coverpage）
在_coverpage.md中使用markdown语法设置。
```markdown
## background image
![](_media/bg.png)

ps:好像不能正常显示本地图片作为的封面背景

## background color
![color](parameter)

ps:color parameter只能是`#2f4253`这种格式。

```

>由于设置封面后，封面与首页同时出现，封面在上，首页在下。使用`onlycover=true`来做到封面首页分离。一般来说，用不到。<br>如果设置了onlycover，则访问README.md需要再原地址后加`README`，即`localhost:xxxx/#/README`

#### 多文件各自独立封面


假如项目目录结构如下
```text
.
└── docs
    ├── README.md
    ├── guide.md
    ├── _coverpage.md
    └── zh-cn
        ├── README.md
        ├── guide.md
        └── _coverpage.md
```
则需要设置封面的有`docs`和`zh-cn`<br>可以在`index.html`中设置<br>
```html
windo.$docsify={
    coverpage:['/','/zh-cn/']
};

//或者

window.$docsify={
    coverpage:{
        '/':'cover.md',
        '/zh-cn/':'cover.md'
    }
};

```

## step 3 配置在github上

<font size=1>首先你得有个github账户以及懂git相关。

然后就可以愉快的开始了。</font>

- 1.搭建一个respository，不要创建README.md。
- 2.clone 到本地
- 3.在本地respository文件夹里使用`docsify init ./projectname`创建项目。
- 4.使用git命令<br>
```Bash
git init //对文件初始化处理
git add ./ //将文件夹添加到发送行列，执行完这一步可能会出来一些replace的话，不用在意。
git status //检查当前状态
git commit -m "message"  //提交
git remote add origin xxxxx/yyy.git //本地仓库与Github上仓库关联，那段xxxyyy就是GitHub仓库名
git push -u origin master //将文件全部推送进远程仓库
```

- 5.在Github选中做文件仓库的respository里点击`setting`，找到`page`。
  - 5.1 *source*选择*Deploy from a branch*——一般无需改动，默认就是这个。
  - 5.2 *Branch*选择*master*,*/(root)*,然后点击*save*，等待一会之后上方就会出现*your site is live at*以及一个网址，这就算成功了。
    - 5.2.1 选择*/docs*也可以，不过容易失败。