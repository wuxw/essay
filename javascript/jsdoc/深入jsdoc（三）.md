##1.    前言

前一篇文章稍微分析了一下JsDoc Rhino，包括如何获取，编译Rhino，以及使用它运行JavaScript脚本。那么这篇文章，我们接着往下分析JsDoc的实现。

##2.    JsDoc项目结构

<pre>
/-
 |--lib
 |--node                --      jsdoc项目需要用到的nodejs模块
    |--fs.js            --      
    |--postinstall.js   --      npm包postinstall事件处理模块
 |--node_modules        --      第三方nodejs模块
 |--plugins             --      
 |--rhino               --      jsdoc定制的mozilla rhino
 |--templates           --      jsdoc文档模板
 |--test                --      jsdoc项目的单元测试
    cli.js              --      
    conf.json.EXAMPLE   --      
    Gruntfile.js        --      grunt配置脚本
    jsdoc               --      bash脚本
    jsdoc.cmd           --      windows bat批处理脚本
    jsdoc.js            --      
    package.json        --      npm包描述文件，包含包名，版本，依赖等
</pre>