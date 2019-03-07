
html -> service.js -> controller.js -> Controller.java -> Service.java -> Dao.java -> mapper.xml -> mysql

web: 运营商管理、商家管理、网站前台

service : 运营商管理、商家管理、广告管理

记录技术点：

1. SOA 
	注册中心 
	  |
	服务层------dubbox-----表现层
	
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
	
	
	