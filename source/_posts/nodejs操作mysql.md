---
title: nodejs操作mysql
date: 2019-01-06 19:39:19
tags:  
	- nodejs  
	- mysql
---



# 使用Nodejs操作mysql数据库

## 基本使用步骤

1. 在npm网站中https://www.npmjs.com/搜索mysql，安装mysql第三方模块，`npm install mysql --save `

2. 引入 mysql, `var mysql = require('mysql')`

3. 阅读文档，看连接接数据库，增删改查如何使用

   官方文档：https://www.npmjs.com/package/mysql/v/2.16.0#introduction



## 连接数据库代码

```javascript
var mysql = require('mysql'); 

//连接数据库参数配置
var connection = mysql.createConnection({
    host    :"localhost", //主机
    port    :'3306',	//端口
    user    :"root",	//用户名
    password:"123456",	//密码
    database:"test"		//数据库
});
//连接mysql
connection.connect(function(err){
    if(err){
        throw err;
    }
    console.log('connect success');
});
```

**连接常用选项**：

- `host`：要连接的数据库的主机名。（默认值： `localhost`）

- `port`：要连接的端口号。（默认值：`3306`）

- `user`：要进行身份验证的MySQL用户。

- `password`：MySQL用户的密码。

- `database`：用于此连接的数据库的名称（可选）。

- `charset`：连接的charset。这在MySQL的SQL级别（如`utf8_general_ci`）中称为“整理” 。如果指定了SQL级别的字符集（如`utf8mb4`），则使用该字符集的默认排序规则。（默认值：`'UTF8_GENERAL_CI'`）

- `socketPath`：要连接到的unix域套接字的路径。使用mac苹果电脑的同学需要设置mysql.sock的路径。

  如：`   socketPath: '/Applications/MAMP/tmp/mysql/mysql.sock' `



## 增删改查操作

- 查询

  ```javascript
  connection.query('select * from article',function(err,rows,fields){
        if(err){
            throw err;
        }
        //success  to do ...
  });
  ```

- 删除

  ```javascript
  connection.query('delete from article where id= 1',function(err,result){
        if(err){
            throw err;
        }
        //success  to do ...
  });
  ```

- 增加

  ```javascript
    var  sql = 'INSERT INTO article(id,title,content) VALUES(0,?,?)';
    var  bind = ['NBA', 'NBANBANBA']; // 数组元素和对应占位符的？号参数绑定
    connection.query(sql,bind,function(err,result){
        if(err){
            throw err;
        }
        //success  to do ...
    });
  ```

- 更新

  ```javascript
    var  sql = 'update  article set title = ?,content = ? where id = ? ';
    var  bind = ['CBA','CBACBACBA',1];
    connection.query(sql,bind,function(err,result){
        if(err){
            throw err;
        }
        //success  to do ...
    });
  ```
