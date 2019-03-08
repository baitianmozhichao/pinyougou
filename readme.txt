
html -> service.js -> controller.js -> Controller.java -> Service.java -> Dao.java -> mapper.xml -> mysql

web: 运营商管理、商家管理、网站前台

service : 运营商管理、商家管理、广告管理

记录技术点：

1. SOA 面向服务
	注册中心 (zookeeper)
	  |
	服务层------dubbox-----表现层
	
	dubbox
	<dubbox:application name /> 、<dubbox:registry address="zookeeper://" />、
	<dubbo:protocol name port />、<dubbo:annotation package />
	服务层 @Service、 表现层@Reference
	
	zookeeper
	zNood: 短暂、持久 create (/hgits mzc) get set delete
	管理(存储，读取)用户程序提交的数据：
	数据节点监听服务 Watch: state、path、type
	Leader & follower 半数选举
	
2. FastDFS图片上传
 	前端：
	使用h5的FormData上传图片组件：
	var formdata = new FormData();
	formdata.append('file', file.files[0]);
	return $http({
		url:'../upload.do',
		method:'post',
		data:formdata,
		headers: {'Content-Type':undefined},
	    transformRequest: angular.identity
	})
	后端：trackerServer + storageServer
	
3. mybatis
	pojo、基本数据类型、hashMap  
	|
	sqlSessionFactory(mybatis-config.xml) -> sqlSession ->  mapper -> executor -> mapperStatement
	|
	pojo、基本数据类型、hashMap  
	
	开启驼峰命名规则、别名、环境选择（enviroment）
	
	sqlSession 一级缓存域 ：相同sql、参数时起效
	mapper namespace是二级缓存域
	
	#{} prepareStatement防sql注入， ${}Statement字符串拼接
	
	resultMap:
	column、property
	一对一：associasion
	一对多：collection
	坑：一对多时，子表id和主表同名时，需要使用as将sql查出的子表id改名，否则mybatis处理成只有一条数据
	
	mybatis-generator dao层代码生成插件
	
4. redis
	String set、get
	list lpush、rpush、lrange
	set sadd、srem、smembers、sismember 
	sorted set zadd、zrange
	hash hmset、hset、hgetall
	rdb:快照，save、stop-writes-on-bgsave-error、rdbcompression、rdbchecksum
	aof:增量，appendonly
	事务：multi、exec、discard、watch
	复制：slaveof、masterauth、slave-read-only、slave-priority
	安全：requirepass、rename-command
	.conf:daemon、database
	
5. Spring容器、SpringMVC容器
	博文：https://blog.csdn.net/wzx104104104/article/details/74937605
	web容器启动过程
	. web应用--->web容器（全局的上下文环境ServletContext，宿主环境）
	
	. web容器启动时，contextLoaderListener 监听并创建了WebApplicationContext接口的实现类
		（例如AnnotationConfigWebApplicationContext）该上下文对象就是IOC容器，
		容器中的bean是定义在web.xml的contextConfigLocation中，该上下文对象会存储在ServletContext中
		
	. Spring容器创建完后，接着创建Servlet，例如前端控制器DispatcherServlet，将放在ServletContext中的WebApplicationContext作为parent上下文，
		创建spring mvc相关的bean，上下文对象会存储在ServletContext中，key与servlet名字有关
	
	联系：ContextLoaderListener中创建Spring容器主要用于整个Web应用程序需要共享的一些组件，比如DAO、数据库的ConnectionFactory等；
		而由DispatcherServlet创建的SpringMVC的容器主要用于和该Servlet相关的一些组件，比如Controller、ViewResovler等。
		子容器(SpringMVC容器)可以访问父容器(Spring容器)的Bean，父容器(Spring容器)不能访问子容器(SpringMVC容器)的Bean。
	
