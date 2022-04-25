本节主要找接收消息的hook地址，需要用到CE和OD工具。附加微信之后，用另外一个微信，给已经登陆的微信发送一条信息，然后用CE 点击：New Scan ，注意不要选 UTF-16，搜索之后，出来了几条结果，再用一个微信发送一条信息，这时看有哪些地址是刚才的发送的内容，把他选到下面去。
![image](https://user-images.githubusercontent.com/96330669/165005161-416b1193-c17e-4bf2-a041-3f8ad58c4e51.png)
然后把下面的value值的长度调长，可以看到最长的里面有msg之类的，基本确定是这个地址
![image](https://user-images.githubusercontent.com/96330669/165005175-120a784c-851a-432e-97ce-7379d044bbb4.png)
然后把这个地址复制下来，在OD里面下个断点，
![image](https://user-images.githubusercontent.com/96330669/165005183-62f46ad9-dee9-4dc3-ac03-cda561e39a73.png)
然后发送一个消息，此时就断下来了，然后删除断点，在右下角的窗口找，找到出现msg类似的信息，点击右键，选“反汇编窗口中跟随”，然后在上面汇编里面下断点，
![image](https://user-images.githubusercontent.com/96330669/165005193-ab531d24-8411-4a99-b1e5-781c55c20bbf.png)
![image](https://user-images.githubusercontent.com/96330669/165005196-b134d2dc-aa91-47bb-b870-654481ce4abb.png)
然后现在发送一个消息，看下断下来了，然后看esp里面东西，可以看到微信id和一些信息，然后计算 esp与wxid和发送内容之间的相对地址，即：[[esp]]+0x40 是微信id或者群id 的地址，[[esp]]+0x68 是消息内容 ，然后也把偏移地址记录下来。
![image](https://user-images.githubusercontent.com/96330669/165005201-fb99f1bc-a4bc-4fa9-b2d6-ae187154ec56.png)
这样就可以得到各种消息通知。
目前已经实现了很多有趣的功能，运行稳定，比如：发各种消息，
接收各种消息，群管，下载文件，加好友，检测僵尸粉，朋友圈等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流，Q：2645542961
![image](https://user-images.githubusercontent.com/96330669/165005265-dd5dfa86-74a8-4263-a020-7e0f08ed1299.png)
