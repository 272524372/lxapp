(function () {
	LConstant = 
	{
			POST:'post',
			GET:'get',
			WEB : "http://172.16.131.158:8080/linktrust",
			TIMEOUT: 15000
	},
    window.linktrust=  {
		/**
		合并属性值,如果第一个参数为true，将合并的属性值放到一个新对象中
		**/
		extend: function(target){
			var len = arguments.length,
				index = 1,
				first = arguments[0];
			if(typeof target == 'boolean'){
				if(target) first = {};
				else{
					first = arguments[1];
					index = 2;
				}
			}
			for(; index < len; index++){
				var o = arguments[index];
				for(i in o) if(o[i] !== undefined) first[i] = o[i];
			}
			return first;
		},
		/**
		显示覆盖层
		**/
		showMask: function(){
			var doc = document,
				div = doc.getElementById('dh_mask');
			if(!div){
				div = doc.createElement('div');
				div.id = 'dh_mask';
				div.className = 'dh_mask';
				doc.body.appendChild(div);
			}
			div.style.display = 'block';
		},
		/**
		获取浏览器厂商的标记
		**/
		getVendor: function(){
			if(typeof linktrust._vendor !== 'undefined') return linktrust._vendor;
			var vendors = 't,webkitT,MozT,msT,OT'.split(','),
				t,
				i = 0,
				l = vendors.length,
				docStyle = document.documentElement.style;

			for ( ; i < l; i++ ) {
				t = vendors[i] + 'ransform';
				if ( t in docStyle) {
					linktrust._vendor = vendors[i].substr(0, vendors[i].length - 1).toLowerCase();
				}
			}
			return csdn._vendor;
		},
		/**
		隐藏覆盖层
		**/
		hideMask: function(){
			var div = document.getElementById('dh_mask');
			if(div) div.style.display = 'none';
		},
		each: function(elements, callback){
			var i, key
			if (typeof elements.length == 'number') {
			  for (i = 0; i < elements.length; i++)
				if (callback.call(elements[i], i, elements[i]) === false) return elements
			} else {
			  for (key in elements)
				if (callback.call(elements[key], key, elements[key]) === false) return elements
			}

			return elements
		},
		showErr : function(ex, title) {
			try {
				var message = [];
				for (i in ex) {
					//if (typeof ex[i] == 'function' || typeof ex[i] == 'object') continue;
					message.push("\n" + i + ":" + ex[i]);
				}
//				plus.statistic.eventTrig("error",message.join(';'));
				//console.trace();
				alert(title + ":" + message.join(';') + ':' + ex.message);
				//plus.console.log(message.join(';'));
				throw ex;
			} catch (err) {
//				alert(ex.type + ':' + ex.message);
//				plus.statistic.eventTrig("error",err.message);
			}
		},
		
		dbName :'linktrust', //数据库名
	    	version : '1.0', //版本信息
	    	description:'linktrust', //描述信息
	    	maxSize : 1024 * 1024 * 1024, //最大值ֵ
	    	dbObj : null,
		 //打开数据库
	     openDB:function() {
	        try {
	            if (!dbObj) {
	                dbObj = openDatabase(dbName, version, description, maxSize);
	            }
	        } catch (e) {
	            alert("打开数据库出现未知错误： " + e);
	            dbObj = null;
	        }
	        return dbObj;
	    },
	
	    getDBconn:function () {
	        openDB();
	        return dbObj;
	    },
	
	    executeSqlDefault : function (sqlStr, params, successHandler, errorHandler) {
	        openDB();
	        dbObj.transaction(function (tx) {
	            tx.executeSql(sqlStr, params, successHandler, errorHandler);
	        }, null, null);
	    },
	
	    executeSqlTrans : function (fun, successHandler, errorHandler) {
	        openDB();
	        dbObj.transaction(fun, errorHandler, successHandler);
	    },
	
	    //修改数据库版本信息
	    changeDBVersion : function (oldVersion, newVersion) {
	        dbObj = openDB();
	        dbObj.changeVersion(oldVersion, newVersion, null, errorFun, null);
	    },
	
	    //判断某表是否存在:表名、存在回调函数、不存在回调函数
	    isExitTable : function (tableName, exitFun, noexitFun) {
	        dbObj = openDB();
	        var sql = "select * from sqlite_master where type='table' and name = ?";
	        dbObj.transaction(function (tx) {
	            tx.executeSql(sql, [tableName], function (transaction, result) {
	                if (result.rows.length > 0 && exitFun) {
	                    exitFun.call();
	                } else if (result.rows.length <= 0 && noexitFun) {
	                    noexitFun.call();
	                }
	            }, null);
	        });
	
	    },
	
	    //删除表数据：表名，删除成功回调函数
	    delTbleData : function (tableName, callBackFun) {
	        dbObj = openDB();
	        var sql = "delete from ?";
	        dbObj.transaction(function (tx) {
	            tx.executeSql(sql, [tableName], callBackFun, null);
	        });
	    },
	
	    //删除表，删除成功回调函数
	    delTbleData : function (tableName, callBackFun) {
	        dbObj = openDB();
	        var sql = "drop table ?";
	        dbObj.transaction(function (tx) {
	            tx.executeSql(sql, [tableName], callBackFun, null);
	        });
	    },
	    jsonpAjax : function(url, method, successCallback, errorCallback)
	    {
	    	if(!!method && method == LConstant.POST) 
	    		 method = LConstant.POST;
	    	else
	    		method = LConstant.GET
	    	
	    	linktrust.ajax({
				type : method,
				timeout : LConstant.TIMEOUT,
				url : url,
				dataType : 'jsonp',
				success : function(data) {
	                    successCallback && successCallback(data);
				},
				error : function(xhr, type, s2) {
					
					if(type == 'abort') return;
					
					if(!!errorCallback)
					{
						errorCallback && errorCallback(data);
					}
					else
					{
						$.alert("发生网络错误，请稍后重试",'错误提示','确定',null);
					}
				}
			});
	    }
    };
})();