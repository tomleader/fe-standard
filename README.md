# fe-standard
simple front-end  standard docs and configs

# 前端项目规范v0.2 --by linktang

***

## 简介

该规范主要的设计目标是希望项目开发的时候大家对开发模式能保持一致，对项目更容易理解并方便构建与管理。
在我看来，前端制定的规范应该考虑至少以下几个方面的内容：
   1. `项目基础结构&命名规范`;
   2. `项目基础库&框架选型`
   3. `项目的基本开发模式或方法`
   4. `项目的基本构建流程`

***

## 基础目录结构规范

### 目录命名原则

1. `简洁`。目录名应该采用容易理解且简短的缩写。下面是例子：
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

***



## FAQ

lastmodified by lintkang


