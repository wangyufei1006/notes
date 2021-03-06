# Android 开发耗电解决方案

![Android开发耗电](http://pic001.cnblogs.com/images/2010/145819/2010101818524169.png)

大部分的电都消耗在了网络连接、GPS、传感器、后台服务上了。

## 解决方案

* 在需要连接网络的模块，**先检测网络连接是否正常**，如果没有连接，则不需要执行网络请求操作
* 进行大数据量下载时，**尽量使用 GZIP 压缩方式下载**，能减少网络流量，减少与服务器连接时间
* **使用效率高的数据格式和解析方法**。
    * 数据解析
        * 树形解析（如DOM）
        * 流的方式解析（SAX）
        * 使用流的方式解析效率要高一些，因为 DOM 解析是在对整个文档读取完后，再根据节点层次等再组织起来；而流的方式是边读取数据边解析，数据读取完后，解析也就完毕了。
    * 数据格式
        * Json
        * XML
        * Protobuf
        * JSON 和 Protobuf 效率明显比 XML 好很多，XML 和JSON 大家都很熟悉，Protobuf 是 Google 提出的，一种语言无关、平台无关、扩展性好的用于通信协议、数据存储的结构化数据串行化方法。尽量使用 SAX 等边读取边解析的方式来解析数据，针对移动设备，最好能使用 JSON 之类的轻量级数据格式为佳。

![](http://pic001.cnblogs.com/images/2010/145819/2010101818531593.png)

* **尽量不要使用 GPS 定位**，可以使用 wifi 和移动网络 cell 定位即可。GPS 定位消耗的电量远远高于移动网络定位。
* 使用**缓存技术**，不需要进行多次请求。
* 后台 service 不要不停的去服务器上更新数据，在不更新数据的时候就让它 sleep，通常情况下，可以**使用 AlarmManager 来定时启动服务**。
* **尽量不要使用浮点运算**
* **回收 java 对象**，特别是较大的 java 对像。
* 在运行你的程序前**先检查电量**，电量太低，那么就提示用户进行充电。
