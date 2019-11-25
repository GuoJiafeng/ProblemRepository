### 查看版本历史
~~~shell
gjf:SharedFS guojf$ git log -3
commit 49a8418d29d8f69e7750ee00a5372c2fcab64ef6 (HEAD -> master, origin/master, origin/HEAD)
Author: GuoJiafeng <18611781163@163.com>
Date:   Mon Nov 25 17:14:39 2019 +0800

    Revert "first commit"
    
    This reverts commit eb7784c0b36dd7eb944578a359ee180a2d758d54.

commit eb7784c0b36dd7eb944578a359ee180a2d758d54
Author: GuoJiafeng <18611781163@163.com>
Date:   Mon Nov 25 17:11:20 2019 +0800

    first commit

commit c4b4ec0539847f7c68c5b1a4a1d785d74d120774
Author: GuoJiafeng <18611781163@163.com>
Date:   Sat Apr 27 22:45:08 2019 +0800

    2019年4月27日22:43:43 fromwin   更新fastjson版本

~~~

### 回滚

~~~shell
git reset --hard e377f60e28c8b84158
~~~



### 强制提交

~~~shell
git push -f origin master
~~~





参考：

https://blog.csdn.net/daocaoren1543169565/article/details/83347100

https://blog.csdn.net/u010286027/article/details/86165291