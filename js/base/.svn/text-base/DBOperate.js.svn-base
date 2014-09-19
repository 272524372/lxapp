/*管理本地sql相关脚本*/

var DBConn = function () {

    var dbName = 'linktrust'; //数据库名
    var version = '1.0'; //版本信息
    var description = 'linktrust'; //描述信息
    var maxSize = 1024 * 1024 * 1024; //最大值ֵ
    var dbObj = null;

      //打开数据库
    function openDB() {
        try {
            if (!dbObj) {
                dbObj = openDatabase(dbName, version, description, maxSize);
            }
        } catch (e) {
            alert("打开数据库出现未知错误： " + e);
            dbObj = null;
        }
        return dbObj;
    }

    this.getDBconn = function () {
        openDB();
        return dbObj;
    }

    this.executeSqlDefault = function (sqlStr, params, successHandler, errorHandler) {
        openDB();
        dbObj.transaction(function (tx) {
            tx.executeSql(sqlStr, params, successHandler, errorHandler);
        }, null, null);
    }

    this.executeSqlTrans = function (fun, successHandler, errorHandler) {
        openDB();
        dbObj.transaction(fun, errorHandler, successHandler);
    }

    //修改数据库版本信息
    this.changeDBVersion = function (oldVersion, newVersion) {
        dbObj = openDB();
        dbObj.changeVersion(oldVersion, newVersion, null, errorFun, null);
    }

    //判断某表是否存在：表名、存在回调函数、不存在回调函数
    this.isExitTable = function (tableName, exitFun, noexitFun) {
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

    }

    //删除表数据：表名，删除成功回调函数
    this.delTbleData = function (tableName, callBackFun) {
        dbObj = openDB();
        var sql = "delete from ?";
        dbObj.transaction(function (tx) {
            tx.executeSql(sql, [tableName], callBackFun, null);
        });
    }

    //删除表，删除成功回调函数
    this.delTbleData = function (tableName, callBackFun) {
        dbObj = openDB();
        var sql = "drop table ?";
        dbObj.transaction(function (tx) {
            tx.executeSql(sql, [tableName], callBackFun, null);
        });
    }
}
