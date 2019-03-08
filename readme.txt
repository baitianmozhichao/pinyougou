
html -> service.js -> controller.js -> Controller.java -> Service.java -> Dao.java -> mapper.xml -> mysql

web: ��Ӫ�̹����̼ҹ�����վǰ̨

service : ��Ӫ�̹����̼ҹ���������

��¼�����㣺

1. SOA �������
	ע������ (zookeeper)
	  |
	�����------dubbox-----���ֲ�
	
	dubbox
	<dubbox:application name /> ��<dubbox:registry address="zookeeper://" />��
	<dubbo:protocol name port />��<dubbo:annotation package />
	����� @Service�� ���ֲ�@Reference
	
	zookeeper
	zNood: ���ݡ��־� create (/hgits mzc) get set delete
	����(�洢����ȡ)�û������ύ�����ݣ�
	���ݽڵ�������� Watch: state��path��type
	Leader & follower ����ѡ��
	
2. FastDFSͼƬ�ϴ�
 	ǰ�ˣ�
	ʹ��h5��FormData�ϴ�ͼƬ�����
	var formdata = new FormData();
	formdata.append('file', file.files[0]);
	return $http({
		url:'../upload.do',
		method:'post',
		data:formdata,
		headers: {'Content-Type':undefined},
	    transformRequest: angular.identity
	})
	��ˣ�trackerServer + storageServer
	
3. mybatis
	pojo�������������͡�hashMap  
	|
	sqlSessionFactory(mybatis-config.xml) -> sqlSession ->  mapper -> executor -> mapperStatement
	|
	pojo�������������͡�hashMap  
	
	�����շ��������򡢱���������ѡ��enviroment��
	
	sqlSession һ�������� ����ͬsql������ʱ��Ч
	mapper namespace�Ƕ���������
	
	#{} prepareStatement��sqlע�룬 ${}Statement�ַ���ƴ��
	
	resultMap:
	column��property
	һ��һ��associasion
	һ�Զࣺcollection
	�ӣ�һ�Զ�ʱ���ӱ�id������ͬ��ʱ����Ҫʹ��as��sql������ӱ�id����������mybatis�����ֻ��һ������
	
	mybatis-generator dao��������ɲ��
	
4. redis
	String set��get
	list lpush��rpush��lrange
	set sadd��srem��smembers��sismember 
	sorted set zadd��zrange
	hash hmset��hset��hgetall
	rdb:���գ�save��stop-writes-on-bgsave-error��rdbcompression��rdbchecksum
	aof:������appendonly
	����multi��exec��discard��watch
	���ƣ�slaveof��masterauth��slave-read-only��slave-priority
	��ȫ��requirepass��rename-command
	.conf:daemon��database
	
5. Spring������SpringMVC����
	���ģ�https://blog.csdn.net/wzx104104104/article/details/74937605
	web������������
	. webӦ��--->web������ȫ�ֵ������Ļ���ServletContext������������
	
	. web��������ʱ��contextLoaderListener ������������WebApplicationContext�ӿڵ�ʵ����
		������AnnotationConfigWebApplicationContext���������Ķ������IOC������
		�����е�bean�Ƕ�����web.xml��contextConfigLocation�У��������Ķ����洢��ServletContext��
		
	. Spring����������󣬽��Ŵ���Servlet������ǰ�˿�����DispatcherServlet��������ServletContext�е�WebApplicationContext��Ϊparent�����ģ�
		����spring mvc��ص�bean�������Ķ����洢��ServletContext�У�key��servlet�����й�
	
	��ϵ��ContextLoaderListener�д���Spring������Ҫ��������WebӦ�ó�����Ҫ�����һЩ���������DAO�����ݿ��ConnectionFactory�ȣ�
		����DispatcherServlet������SpringMVC��������Ҫ���ں͸�Servlet��ص�һЩ���������Controller��ViewResovler�ȡ�
		������(SpringMVC����)���Է��ʸ�����(Spring����)��Bean��������(Spring����)���ܷ���������(SpringMVC����)��Bean��
	
