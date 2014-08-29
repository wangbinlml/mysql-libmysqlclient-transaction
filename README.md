node-mysql-libmysqlclient-transaction-
======================================

nodejs modules node-mysql-libmysqlclient 事务处理模块


用法：
=====================================


var Mysql = require('mysql-libmysqlclient');
var transaction = require(__dirname + '/transaction.js');
var client = Mysql.createConnectionSync(
    '192.168.109.40',
    'root',
    'root',
    'idmp',
    3306
);
var sql1 = 'insert into test(name) values("333")';
var sql2 = 'insert into test(name) values("4444")';
const DEBUG = true;
transaction(client, DEBUG);
var trans = client.startTransaction();
function error(err) {
    if(err && trans.rollback) {
        trans.rollback();
        console.trace(err);
        //throw err;
    }
}
trans.query(sql1, error);
trans.query(sql2, error);
trans.commit();
console.log("success!");
console.log("mysql-queues: An exception occurred for this query:\n\t",
    sql1);
    */
/*
var sql1 = 'START TRANSACTION';
var sql2 = 'insert into test(name) vdalues("333")';
var sql3 = 'insert into test(name) values("4444")';
var sql4 = 'COMMIT';
var sql5 = 'ROLLBACK';
try{
    conn.querySync(sql1);
    conn.querySync(sql2);
    conn.querySync(sql3);
    conn.querySync(sql4);
}catch(error){
    conn.querySync(sql5);
    console.log(error.stack);
}
*/
