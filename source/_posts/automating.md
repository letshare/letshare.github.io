title: automating  workflow
date: 2014/08/20 22:14:10
tags: ['automating']
categories: 效率
---

开发一个web项目可能会。。。
![](/img/automating/slide_2.jpg)
需要掌握的知识越来越复杂。。。  
boilerplate abstractions frameworks testing docs workflow dependency management performance   optimization build continuous integration   
deployment version control   

时间是保持效率的关键。。。

怎么做节省你的时间？

自动构建重复的任务让你的工作保持效率！

自动化阐述的不是懒惰，而是效率！

![](/img/automating/slide_13.jpg)


好的工具可以产生巨大的生产力，艺术家or泥瓦工？


![](/img/automating/slide_15.jpg)

对前端攻城狮来说，一般的工作流程是这样的：

**初始化一个项目**  
搭建过程  
下载 libraries  
下载 templates  
下载 frameworks  

**开发过程**  
Sass/Less/Stylus  
CoffeeScript    
Jade/Haml  
LiveReload  
JS/CSS Linting  

**部署环节**  
代码检查  
单元测试  
编译代码  
压缩和合并  
生成图片和图标  
性能优化  
HTTP服务  
发布服务  

你可能用到一些工具自动构建一些小项目

codekit    
hammar  
prepros  
koala-app  
mixture  
compass  
scout  

持续的提升  
First Do it.  
Then do it right.  
Then do it better.  

怎样才能更好呢？

所有项目适用的自动化构建流程

![YEOMAN](/img/automating/slide_34.jpg)

Yo 让搭建框架代码更少  
Grunt 帮助部署、预览、测试  
Brow 帮助管理依赖  

![](/img/automating/slide_36.jpg)

根据你的要求弹性地自定义初始化工作  
减少写模板的时间  
增加开发过程的效率和乐趣  

![Grunt](/img/automating/slide_40.jpg)

帮助运行重复的任务

Linting  
Compiling  
Minification  
Testing  
Conversion  
Documentation  
Deployment  
And More  

你可能会选择其他的 Rake/Cake/Make/Ant

![Grunt](/img/automating/slide_44.jpg)

Grunt 只需要配置好两个文件 package.json Gruntfile.js

package.json指定插件和元信息。
```javascript
{
	name:"awesome-app",
	version:"0.0.1",
	devDependencies:{
		grunt:"~0.4.5",
		grunt-contrib-jshint:"~0.10.0",
		grunt-contrib-uglify:"~0.6.0"
	}
}
```

Gruntfile.js配置任务和加载插件
```javascript
module.exports = function(grunt){
	grunt.initConfig({
		uglify:{
			build:{src:'app.js',dest:'build/app.min.js'}
		},
		jshint:{
			all:['**/*.js']
		}
	});

	grunt.loadNpmTasks('grunt-contrib-uglify');
	grunt.loadNpmTasks('grunt-contrib-jshint');
	grunt.registerTask('default',['uglify','jshint']);
};
```

```shell
$ npm install -g grunt-cli
$ npm install
$ grunt 
Running "uglify:build"(uglify)task
Running "jshint:all"(jshint)task
Done.
```

![](/img/automating/not-bad.jpg)

```shell
$ npm install grunt-<taskname> --save-dev
```

task tip  
**grunt-responsive-images**  
生成多种尺寸的图片  

task tip  
**grunt-contrib-imagemin**  
优化图片可以让你的页面更"轻"  

speed tip  
**grunt-concurrent**  
同时跑一些比较慢的任务Sass、Coffee，可以显著的提供你的构建速度。  

speed tip  
**grunt-newer**  
只有原文件在上一次任务之后改动过才重新运行任务。  

你是否遇到类似的情况，使用了bootstropUI框架，实际上你的页面只用了bootstrop不到了10%的css样式。  
可以使用devTools分析页面。  
![](/img/automating/audits.png)

**grunt-uncss**  
可以在build的时候去除那些没用到的css。  
then，那些几百k的css文件就可以精简为很小的css，提供页面的渲染性能。

![Bower](/img/automating/slide_70.jpg)

web项目的包工具

老旧的方式是怎么管理包的呢
1. 上一次升级包是6个月前，要升级下了
2. 打开网站
3. 下载包
4. 复制到自己的项目中
5. 然后拼命找项目中用到包的地方，改引用

新的方式

```shell
$ npm install -g bower
$ bower search angular
$ bower install angular --save-dev
bower not-cached    git://github.com/angular/bower-angular.git#*
bower resolve       git://github.com/angular/bower-angular.git#*
bower download      https://github.com/angular/bower-angular/archive/v1.2.25.tar
.gz
bower progress      angular#* received 0.4MB of 0.4MB downloaded, 97%
bower extract       angular#* archive.tar.gz
bower invalid-meta  angular is missing "ignore" entry in bower.json
bower resolved      git://github.com/angular/bower-angular.git#1.2.25
bower install       angular#1.2.25
bower no-json       No bower.json file to save to, use bower init to create one

```
包下载在当前目录/bower_components/包。

安装命令有这几种：
```shell
$ bower install
$ bower install <package>
$ bower install <package>#<version>
$ bower install <name>=<package>#<version>
```

```shell
$ bower list
bower check-new     Checking for new versions of the project dependencies..
letshare.github.io d:\xuntuu\letshare.github.io
└── angular#1.2.25 extraneous (1.2.26-build.468+sha.a365152 available, latest
 is 1.3.0-rc.2)
```
运行基于：
+ Git
+ HTTP(s)
+ Zip
+ npm

嘿嘿，从此几行命令，就可以解决依赖问题了

**grunt-bower-install**
```shell
$ npm install grunt-bower-install --save-dev

```