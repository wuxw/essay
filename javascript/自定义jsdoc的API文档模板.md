#自定义jsdoc的API文档模板#

分析grunt-jsdoc插件下的jsdoc这个批处理脚本：

	node_modules/grunt-jsdoc/node_modules/jsdoc

我们可以发现其最终执行的是这行命令：

	java -classpath "${BASEPATH}/rhino/js.jar" ${CMD} -opt -1 -modules "${URLPATH}/node_modules" -modules "${URLPATH}/rhino" -modules "${URLPATH}/lib" -modules "${URLPATH}" "${BASEPATH}/jsdoc.js" "$@" --dirname="${BASEPATH}/" 

由此我们可以推测，整个jsdoc文档生成程序的执行路口就是jsdoc.js这个文件。

通过分析这个文件我们可以找到以下代码：

	jsdoc.util.include(env.opts.template + '/publish.js');

grunt-jsdoc配置：

	jsdoc: {
            dev : {
                src: jsdoc_src, 
                options: {
                    template : 'templates/ebaui',
                    private    : false,
                    destination: 'dev_release/doc/',
                    tutorials  : 'dev_release/demo'
                }
            }
        }

jsdoc内部使用了[TaffyDB-The JavaScript Database](http://www.taffydb.com/)