#### 一、图灵智盒-消息通（软件版）系统安装说明

**视频安装教程：**

https://www.bilibili.com/video/BV1XXHrzCEuv/

**官网：**

https://wechat666.com

**功能描述：**

实现个人微信消息发送接口，可以通过访问数据库或api接口调用，实现给个人微信发送消息，给微信群发送消息； 用于智慧水利、水利数字孪生中水位预警、监测提醒；流量预警监测提醒；设备报警、操作记录提醒； 工业传感器数据监测、预警提醒； 各类业务系统待办提醒等。 docker 跨平台部署。

**安装过程：**

##### 1、确保您的运行环境安装有docker

##### 2、拉取镜像

```
#拉取镜像
docker pull crpi-qid0xtviugr6gnax.cn-hangzhou.personal.cr.aliyuncs.com/wechat666/msg:v1.0

#重命名镜像
docker tag crpi-qid0xtviugr6gnax.cn-hangzhou.personal.cr.aliyuncs.com/wechat666/msg:v1.0 wechat666:v1.0

```

##### 3、创建容器并运行

```
#创建并运行容器
docker run -d -p 6080:80 -p 5306:3306 -p 8093:8093 --name wechat wechat666:v1.0
```

##### 4、打开浏览器，访问管理界面，配置授权码

打开浏览器输入 http://127.0.0.1:6080 其中127.0.0.1是部署docker机器的ip地址，6080是 上面 docker run 中的6080，可以自定义修改。打开后，双击里面的 license.txt , 然后将从官网https://wechat666.com中注册、登录 购买的 授权码 拷贝、粘贴到里面

![image-20250909151506124](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909151506124.png)

![image-20250909153554949](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909153554949.png)

![image-20250909153853617](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909153853617.png)

![image-20250909154030622](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909154030622.png)

##### 5、重启容器实例

```
docker restart wechat
```

##### 6、刷新刚才浏览器打开的 http://127.0.0.1:6080 微信扫码登录

等待20秒左右，用手机微信扫码登录微信



##### 7、发消息

方式一、数据库连接方式

1）打开navicat数据库连接工具，连接容器实例中自带的数据库

```
主机：127.0.0.1    #docker 部署机器的ip
端口：5306         #docker run中可以修改
用户名：root		
密码：1234qwer
```

![image-20250909154818763](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909154818763.png)

2）进入后，打开msg_data库，打开t_sms_real表，手动写入一条数据（只需填 msg字段和target字段）

```
msg：消息字段，填写您要发送的消息
target：微信上接收人的名称 或 群的名称
```

![image-20250909155331441](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909155331441.png)

3）查看微信是否接收到该消息



方式二、API调用方式发送消息

```
请求地址：http://127.0.0.1:8093/root/data_gen/send_msg
请求方式：POST
参数：
msg：消息字段，填写您要发送的消息
target：微信上接收人的名称 或 群的名称

注意，参数格式要么是query格式参数，要么是body中的form-data格式； 请求地址中 127.0.0.1是 docker安装机器的ip

```

![image-20250909155904247](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250909155904247.png)

发送后，查看微信是否收到消息。



