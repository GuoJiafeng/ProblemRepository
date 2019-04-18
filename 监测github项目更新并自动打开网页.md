

重要：



~~~http
https://api.github.com/repos/GuoJiafeng/ProblemRepository
~~~





描述问题
想跟踪一个github项目,如果该项目更新了,自动打开网页.

拆解问题
监测github项目更新,更新的标志是什么 
监测网页数据变化在于对比变化 
如何获取网页资源: 
接口API -> json
爬虫 xml 
如果有API就尽量用API,不爬虫.
如何打开网页
import webbrowser
webbrowser.open(url)
1
2
github API使用 
如何阅读API文档,如何使用 
如何利用什么库处理网页内容,提取出自己需要的字段. 
使用requests库下载网页, 持续运行while

import requests
all_info = requests.get(api).json()
# requests.get(api),返回的是状态响应码(eg.200), 使用json()转化数据格式为字典
1
2
3
通过字段之间的对比,来判断github项目是否更新了 
如果更新了, 就打开网页.

代码

import requests
import webbrowser
import time
api_url = "https://api.github.com/repos/channelcat/sanic"
github_url = "https://github.com/channelcat/sanic"

# get_data -> diff_data -> open url
all_info = requests.get(api_url).json()
old_time = None
# old_time = "2016-06-08T12:30:07Z"
# 为了测试程序,可以先给old_time赋值
while True:
    new_time = all_info["updated_at"]
    if not old_time:
        old_time = all_info["updated_at"]
    if new_time > old_time:
        old_time = new_time
        webbrowser.open(github_url)
    time.sleep(100)

---------------------
作者：seekun 
来源：CSDN 
原文：https://blog.csdn.net/tmsshikun/article/details/80968442 
版权声明：本文为博主原创文章，转载请附上博文链接！