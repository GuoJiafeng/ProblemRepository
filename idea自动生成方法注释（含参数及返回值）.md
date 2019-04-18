原文：https://blog.csdn.net/yuruixin_china/article/details/80933835

亲测可用





~~~
*
 * 
 * $VAR1$ 
 * $params$ * @return $returns$
 * @author yuxin
 * @creed: Talk is cheap,show me the code
 * @date $date$ $time$
 */
~~~

~~~groovy
groovyScript("def result=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList(); for(i = 0; i &lt; params.size(); i++) {result+='* @param ' + params[i] + '\\t' + ((i &lt; params.size() - 1) ? '\\n' : '')}; return result", methodParameters())
~~~

