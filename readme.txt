
html -> service.js -> controller.js -> Controller.java -> Service.java -> Dao.java -> mapper.xml -> mysql

web: ��Ӫ�̹����̼ҹ�����վǰ̨

service : ��Ӫ�̹����̼ҹ���������

��¼�����㣺

1. SOA 
	ע������ 
	  |
	�����------dubbox-----���ֲ�
	
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
	
	
	