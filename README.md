# SQL-Chart ��BI����



## һ�����
SQL-Chart����BI���ߣ�ִ��SQL��Ȼ�󽫲�ѯ���������ͼ��ͱ��չʾ����֧��Druid��MySQL�����ǿ���ͨ�����������֧�ֶ�����ʽ������Դ����ʵ�á�

## ��������
### 1������Server
#### demo ����
```node index.js```
#### mysql ����
```node index.js mysql```
#### druid ����Դ
```node index.js druid```

### 2������
```
http://localhost:9090/index.html
```

## ��������
### 1��MySQL����Դ
`server.js`
```
var Q=require('q');
var mysql=require('mysql');
var config={    
			host:'127.0.0.1',       
			user:'root',               
			password:'root',
			port: '3306',
			database:'perftrace'
};
var conn=mysql.createConnection(config);
conn.connect();
//conn.end();

var DBase={
    query:function(sql) {
        var defer=Q.defer();
		conn.query(sql, function(err, rows, fields) {
			if(err){
				defer.reject(err);
			}else{
				defer.resolve(rows);
			}
		}); 
		return defer.promise;
	 }
}
module.exports=DBase;
```
`client.js`
```
!function($,win){
	
	var url='http://127.0.0.1:9090/db/query';
	
	var query=function(sql){
		return execute(url,sql);
	};
	
	
	function execute(url,sql,method){
		return $.ajax({
			url: url,
	        type: method||'POST',
	        data:JSON.stringify({sql:sql}),
	        contentType: 'application/json',
	        dataType: 'json'
	   });
	}
	win.DBClient={query:query,type:'mysql'};
	
}(jQuery,window);

	
/**
 * data=[
 * 		  {x:x,y:y,legend:legend},
 *  	  {x:x,y:y,legend:legend},
 *  	  {x:x,y:y,legend:legend},
 *  	  {x:x,y:y,legend:legend},
 *  	  {x:x,y:y,legend:legend}
 *      ]
 */
	

```



