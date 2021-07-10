# 留学数据爬取
### 本库包括了四个爬虫，分别爬取：寄托天下、一亩三分地、ChaseDream以及新浪微博。

整体的格式是按照这个库来写的：https://github.com/DolorHunter/1p3aMSCSAdminReport 。

#### 一亩三分地
一亩三分地基本就是照搬上面的库，详细的可以看一下上面的这个库是如何运行的。唯一的问题就是触发bot检测机制了。我基本上是爬一页就停10-20分钟，这样的话只是到时检测一下bot即可，不会封号，如果停的时间没有这么长，大概率是直接封号。

#### 寄托天下
寄托天下的爬虫是在一亩三分地的基础上改的。一亩三分地可能会被官方从远程手动关闭连接，这个时候换个IP地址，继续跑就行了。因为寄托不存在看信息需要积分的情况，所以不存在封号的问题。
##### 更新
最近一亩三分地将网页更新成了动态的模式，按照之前的代码所爬下来的是一个动态的内容，具体为<span>标签中的内容，大概的格式为{{i.schollname这样一个格式}}。
解决这个问题的方法为：
1.使用F12开发者工具中的网络部分找到获取用户数据的post XHR文件，具体名字为detail，点开这个XHR去看她的Preview就能看到录取的信息。
2.去构造Header，最重要的部分就是form-data中的那个ID，通过这个ID可以定位到offer信息，如果这个ID没填对得到的response会是 message：offer不存在或已被删除。这里可以用postman这个工具来post请求，根据上面的返回就可以知道Header构建的对不对。
3.如何获得ID呢？我在元素中搜索这个form-data中的id，只会在一个script中找到一个匹配值，利用正则匹配将这个id值匹配出来即可。目前来说，每一次打开offer页面都会对应的生成一个专属的id，在一定时间内都可以通过这个id访问。


#### ChaseDream和weibo
这俩就没啥好说的了。
