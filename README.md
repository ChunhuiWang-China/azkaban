
#azkaban 安装步骤

使用的是azkaban 3.5，java 8 编译而来

## 第一步 解压复制文件

```
tar zxvf 4个tar.gz 
分别copy solo 中的conf，plugins 文件到web 和 executor中
```

## 第二步 设置java环境和mysql

```
java 环境变量设置
mysql 数据库安装
mysql 中创建 azkaban数据库
之后使用 db 中的create－all.sql 来创建所需要的表
```

## 第三步 在web的根目录创建ssl

```
keytool -keystore keystore -alias jetty -genkey -keyalg RSA

password 和 keypassword 需要设置
语言选择：CN  并确认Y
```

## 第四步 进入web／conf设置


```
azkaban.properties 文件
#时区设置
default.timezone.id＝Asia／Shanhai
#数据库设置
database.type=mysql
mysql.port=3306
mysql.host=主机ip
mysql.database=数据库名
mysql.user=用户名
mysql.password=用户密码
mysql.numconnections=100
#ssl
jetty.ssl.port=44444 浏览器访问端口
jetty.port=8081
jetty.keystore=keystore
jetty.password=password
jetty.keypassword=keypassword
jetty.truststore=keystore
jetty.trustpassword=password
#Executor
executor.host = Executor启动ip
#mail
mail.sender=IT@xxx.com
mail.host=smtp.exmail.qq.com
mail.user =IT@xxx.com
mail.password=邮箱密码
job.failure.email=IT@xxx.com
```

#第五步 创建conf下日志log4j.properties 

```
log4j.rootLogger=INFO,C
log4j.appender.C=org.apache.log4j.ConsoleAppender
log4j.appender.C.Target=System.err
log4j.appender.C.layout=org.apache.log4j.PatternLayout
log4j.appender.C.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n  
```

#第六步 启动azkaban

```
./bin/azkaban-web-start.sh 
```

#第七步 executor设置

```
conf目录下
# Azkaban UserManager class
user.manager.class=azkaban.user.XmlUserManager
user.manager.xml.file=conf/azkaban-users.xml
# Loader for projects
executor.global.properties=conf/global.properties
azkaban.project.dir=projects
#DB
database.type=mysql
mysql.port=3306
mysql.host=IP
mysql.database=数据库名
mysql.user=用户名
mysql.password=密码
mysql.numconnections=100
# Velocity dev mode
velocity.dev.mode=false
# Azkaban Jetty server properties.
# Azkaban Executor settings
executor.port=12000 要与web的一致
executor.host= 与web一致
# mail settings
lockdown.create.projects=false
cache.directory=cache
# JMX stats
jetty.connector.stats=true
executor.connector.stats=true
# Azkaban plugin settings
azkaban.jobtype.plugin.dir=plugins/jobtypes   
```

#第八步 同样conf 添加log4j.properties 

```
log4j.rootLogger=INFO,C
log4j.appender.C=org.apache.log4j.ConsoleAppender
log4j.appender.C.Target=System.err
log4j.appender.C.layout=org.apache.log4j.PatternLayout
log4j.appender.C.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n  

```
