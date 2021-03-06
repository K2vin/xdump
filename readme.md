

# xdump.py

### Disclaimer

```
[!] legal disclaimer: Usage of xdump.py for attacking targets without prior mutual consent is illegal.
It is the end user's responsibility to obey all applicable local, state and federal laws. 
Developers assume no liability and are not responsible for any misuse or damage caused by this program
```

### Usage

```
python3 xdump.py
```

### About

```
xdump.py是一个python3下的脱库脚本,只要提供一句话webshell和相关密码就可脱库,与一般大马脱库的区别在于这里的脱库可
订制,可灵活变换代码以绕过waf,相当于用chopper的思路来脱库,不过脱库方法可订制,且比一般大马的脱库更好用,理论上
xdump.py可脱任意大小的数据库,不用担心会超时,因为xdump采用的是每次只脱部分少量数据[eg.每次脱200条数据],也可在代
码中设置每次延时一定时间再继续脱少量数据.
```

### Detail

#### 支持两种脱库用法

```
1.不抓包模式
不抓包模式目前仅测试过mysql+php的脱库,其他类型应该暂不支持,因为不抓包模式用的是固定的php连接数据库的代码

2.抓包模式
抓包模式支持菜刀支持的所有数据库和脚本组合类型的脱库,需要抓包才能用.抓包方法如下:

a.chopper连上webshell
b.charles设置好本地sock5代理.[eg.127.0.0.1:8889]
c.proxfier设置chopper的代理为charles提供的127.0.0.1:8889
d.在chopper中配置好数据库连接参数并连接数据库
e.在chopper连上数据库后随便双击某个数据库的某个表
f.将e步骤在charles中抓取的包整理下存放在本地,整理的格式在代码中有示例,需要提供header和post两份数据,示例文件如下
link:https://github.com/3xp10it/xdump
g.运行python3 xdump.py
```

#### 支持两种脱库速率

```
1.要脱的数据库的表有主键时(如uid,id等),这种情况会根据主键脱库,这种脱库速率与下面的第2种速率相比有较大优势,尤其是在要脱的
数据库的表的条目比较多的时候

2.要脱的数据库的表没有主键时,这种情况会根据limit关键字来依次脱库,这种情况在数据表条目较多的时候比较缓慢,数据库
查询语句性能低,但是数据表没有主键的时候只能这样来脱了
```

#### 支持断点续脱

```
支持脱库中断后断点续脱,断点续脱需要在代码中修改count值,并要保证start=everyQueryCount*count+1为继续dump的起始点的值
[eg.每次查询为200,则要保证200*count+1=新起点dump处],运行之前只需要改count
```
