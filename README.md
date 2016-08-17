

# 前端项目编码规范v0.2

***

## 简介

该规范主要的设计目标是希望项目开发的时候大家的编码风格保持一致，对项目更容易理解，并方便以后维护与管理。
主要包含以下几个方面的内容：
   1. `项目基础结构&命名规范`;
   2. `js书写规范`
   3. `html或模板书写规范`
   4. `项目的基本构建流程`

***

## 项目基础结构&命名规范


### 项目命名原则

1. `简洁`。目录名应该采用容易理解且简短的缩写,且全部采用小写方式, 以下划线分隔。例如cos,cdn,cdn_new,single_project


### 目录命名原则

1. `简洁`。参考项目命名规则，目录名也应该采用容易理解且简短的缩写。下面是具体例子：
    1. `js`: javascript脚本。 不推荐使用`script`、`scripts`。
    2. `css`: 样式表。 不推荐使用`style`、`styles`等。
    3. `img`: 图片目录。 不推荐用`images`、`imgs`等。
    3. `html`: html文件目录
    4. `src`: 源文件目录。 不推荐使用source;
    5. `lib`: 引入的第三方底层库目录。比如jquery,seajs等，这个目录下的文件应该是多个项目共有的;
    6. `module`: 模块化的主目录，里面应包含多个强业务相关的子目录;例如cvm业务统计模块
    7. `common`： 模块化的主目录，里面应包含多个弱业务相关的子目录（业务共有模块目录）;例如路由模块，图片浮层模块
    7. `util`： 各种通用工具类的主目录，里面应包含多个通用的工具模块;例如date处理，string处理等,util模块应处于module和common目录的下一级;
    7. `doc`： 存放项目相关文档
    7. `tpl`： 存放模板文件的目录，这里建议按模块划分，即每个大的模块内自带tpl目录，模板文件建议格式为xxx.html或xxx.htm
    7. `conf`： 主配置目录，里面应包含项目相关的一些基础配置文件
    8. `server`:服务器端相关文件的存放目录，这部分目录内的文件应该不能直接通过web方式访问;
    8. `gulp`:gulp相关配置文件的存放目录
    8. `bin`:服务器端相关可执行文件的存放目录，这部分目录内的文件应该不能直接通过web方式访问;
    8. `dist`:项目发布文件的目录，这部分目录的内容是发布到生产环境的内容;
    8. `test`:用于存放测试假数据或者测试用例的目录，非必须;
    8. `build`:项目构建所需可执行文件的存放目录，这部分目录内的文件应该不能直接通过web方式访问;


### 目录结构划分

#### 一级目录划分
这里定义根目录是${root}，则常用的一级目录有`js`、`css`、`html`、`test`等，页面较少的时候，html文件可单独与一级目录并行。下面是例子：

    ${root}/
        js/
        css/
        img/
        doc/
        index.html
        error.html
        ...

如果html文件过多，则应该考虑单独划分一个目录：

    ${root}/
        js/
        css/
        img/
        doc/
        html/
            index.html
            error.html
            xxx.html
        ...

假如项目自身是一个纯js的项目，则可省略js一级目录，下面是例子(mod表示模块)：

    ${root}/
        src/
            common/
            mod1/
                submod1/
                submod2/
                submod3/
            mod2/
        ...

#### 二级目录级以下的划分

目录划分原则

1. js文件按具体业务模块分类，每个模块内允许出现多个js模块;
2. 为方便组件管理，模块化的js目录下允许出现`css`、`tpl`、`img`等目录，但不需要出现js目录;
3. 尽量避免在一个路径里出现多个src目录

对于一个包含其他静态资源的组件模块，结构应该类似下面的例子：

    mod1/
        img/
            xxx.png
            yyy.png
        css/
            xxx.css
            yyy.css    
        tpl/
            add.tpl.html
        doc/
            readme.doc 
        src/
            mod1-main.js
            mod1-util.js
            mod1-xxx.js
            ...
        index.js         

#### 业务项目目录划分一个比较完整的示例

    ${root}/
        js/
            common/
                dialog/
                    src/
                        tpl/
                            dialog.tpl.js
                            dialog.tpl.html
                            xxx.tpl.js
                        init.js
                        main.js
                        xxx.js
                    index.js
                    img/
                        sprites.png
                        dialog.png
                        xxx.png
                    css/
                        dialog.css
                        bg.css
                        xxx.css  
                upload/
                report/
                ......
            module/
                submod1/
                    src/
                        submod1.main.js
                        submod1.xxx.js
                    index.js
                submod2/
                    subsubmod1/
                        src/
                            tpl/
                                xxx.tpl.js
                            xxx.js
                        index.js    
                    subsubmod2/
                 submodx/
                 ......   
               
        css/
            main.css
            bg.css
            xxx.css
        img/
            logo.png
            xxx.png            
        doc/
            readme.md
            xxxxx.doc
        html/
            index.html
            main.html
        package.json
        readme.md    
        ......


### 文件命名原则

1.参考项目命名原则，例如js文件可以写作index.js, index_en.js
2.文件编码统一使用UTF-8且保证无BOM

***
## js书写规范(ES5)


###变量命名
1.普通变量使用驼峰命名法
```js
// bad
var projectname;

// good
var projectName;
```
2.常量全部大写，如果有多个单词用下划线分割
```js
// bad
var defaultErrCode = -1;

// good
var DEAFULT_ERR_CODE = -1;
```
3.构造函数第一个字母大写
```js
// bad
function person(name) {
    this.name = name;
}

// good
function Person(name) {
    this.name = name;
}
```


###缩进
缩进使用tab（4个空格长度）

###空格
1.对象属性冒号后加空格，前面不加
```js
// bad
var a = {
    b :1
};

// good
var a = {
    b: 1
};
```
2.代码块花括号{左侧需要一个空格

```javascript
// bad
if (condition){
}

while (condition){
}

function funcName(){
}

// good
if (condition) {
}

while (condition) {
}

function funcName() {
}

```
3.函数多个参数之间要有空格
```
// bad
var doSomething = function(a,b,c) {
    // do something
};

// good
var doSomething = function(a, b, c) {
    // do something
};

```
4.if, else, for, while, do, switch, case, try, catch, finally, return, typeof 关键词后必须有空格
```
// bad
var doSomething;
if(doSomething){
    // do some..
}else{
    // else...
}

// good
var doSomething;
if (doSomething){
    // do some..
} else {
    // else...
}
```
5.数组和对象里的元素,`{}` 和 `[]` 内紧贴括号部分不允许包含空格，数组多个元素考虑换行
```javascript
// bad
var arr1 = [ ];
var arr2 = [ 1, 2, 3 ];
var obj1 = { };
var obj2 = { name: 'obj' };
var obj3 = {name: 'obj', age: 20, sex: 1};

// good
var arr1 = [];
var arr2 = [1, 2, 3];
var obj1 = {};
var obj2 = {name: 'obj'};
var obj3 = {
    name: 'obj',
    age: 20,
    sex: 1
};
```
6.单行注释符号必须跟一个空格，多行注释最少3行且*号后面需要一个空格
```javascript
// bad
//这是一个不好的单行注释
var arr1 = [ ];

/*
 *no space after '*', bad example
 */
var x = 1;

// good
// 这样的注释是OK的
var arr2 = [];

/*
 * one space after '*', it is good
 */
var x = 1;

```


###换行
1.每行最多120个半角字符;

2.代码块'{'后和'}'前需要换行, 代码块'{'前不要换行
```
//bad
function test()
{
    // ...
}
//bad
if (condition) {
    // ...
} 
else {
    // ...
}


//good
function test() {
    // ...
}

//good
if (condition) {
    // ...
} else {
    // ...
}

```

3.多个参数或元素需要换行的时候，保证逗号结尾换行
```
//bad
var arr = [1,2,3,4,5,6
,7,8,9,10]

//good
var arr = [1,2,3,4,5,
            6,7,8,9,10]

```

4.连续的函数调用的时候，保证换行后.在前面
```
//bad
var dom = $("body").find(".area").
children().eq(0);

//good
var dom = $("body").find(".area")
    .children().eq(0);

```

5.函数定义结束，或者逻辑上有区分的代码块，需要换行
```
//bad
var f = function() {
    // ...
}
var f2 = function() {
    // ...
}

//good
var f = function() {
    // ...
}

var f2 = function() {
    // ...
}

```

###引号
1.正常使用情况下统一使用单引号' 对象属性正常情况不需要引号，如果确实需要引号则都要加上单引号
```
// bad
var util = require("cos/lib/util");
var str = "str";
var obj = {
	"a": 1
}

// good
var util = require('cos/lib/util');
var str = 'str';
var obj = {
	'a': 1
}
```

###代码风格检查工具

1.统一使用Eslint，配置文件参考本项目的.eslintrc.json

2.提交代码之前必须解决所有Eslint提示错误的地方，解决之后再提交，大家互相监督，有犯错的话请吃饮料；


## FAQ

LastModified by lintkang


