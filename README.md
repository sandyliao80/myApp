# myApp
月光倾城的app应用，将会包含小说，todolist，存钱罐等很多的功能

##使用技术
+ 前端	`Angular`、`ionic`
+ 后台	`nodejs`

##开始日期
2016-07-31 09:45

##起始原因
阿里面试

##运行
+ nodeServer
nodeServer基于IBM的strongloop, 运行前请先安装strongloop，方法如下：
`npm install -g strongloop`
运行项目的话只需要 slc run 就可以了。如果是普通的node程序，在项目目录下npm install就可以了。

+ ionic
运行ionic需要先安装ionic：
`npm install -g cordova ionic`
启动项目只需要ionic serve就可以了



##关于nodejs后台的使用
后台的用户管理用的是strongloop的loopback工具（用它搭建一个用户系统十分的方便）。
你只需要切换到nodejs/xiaodiTodoList目录`npm install`然后修改一些配置文件：
1. `/nodejs/xiaodiTodoList/server/datasources.json`：
```
{
  "db": {
    "name": "db",
    "connector": "memory"
  },
  "mongodb": {
    "host": "localhost",
    "port": 27017,
    "url": "mogodb://username:password@host:port/dbname",
    "database": "dbname",
    "password": "password",
    "name": "mongodb",//第一下输入的名字
    "user": "username",
    "connector": "mongodb"
  }
}
```
然后修改`/nodejs/xiaodiTodoList/server/model-config.json`中所有`db`为你命名的数据库`mongodb`  
可能还需要安装下loopback-connector-mongodb

2. 如何新建自己的方法，比如我新建一个sayHi方法：
在`/nodejs/xiaodiTodoList/server/models/andylistudio-user.js`文件中如下写到:
```
module.exports = function(Andylistudiouser) {
    //声明方法，使用callback return
    Andylistudiouser.sayHi = function(callback) {
        callback(null, 'hi, welcome to Andylistudio!!');
    };
    //注册方法
    Andylistudiouser.remoteMethod(
        'sayHi', {
            'accepts': [],
            'returns': [
                { 'args': 'results', 'type': 'string' }
            ],
            'http': {
                'verb': 'get',
                'path': '/say-hi'
            }
        }
    );
};
```
然后在`nodejs/xiaodiTodoList/server/models/andylistudio-user.json`配置下方法的权限，否则会出现权限问题：
```
"acls": [
    {
      "principalType": "ROLE",
      "principalId": "$everyone",//所有人可以使用
      "permission": "ALLOW",
      "property": "sayHi"
    }
```

+ datasource.json的mysql配置
  "mysql-remote": {
    "host": "qdm1300839.my3w.com",
    "port": 3306,
    "url": "mysql://qdm1300839:121960425sql@qdm1300839.my3w.com/qdm1300839_db",
    "database": "qdm1300839_db",
    "password": "121960425sql",
    "name": "mysql-local",
    "user": "qdm1300839",
    "connector": "mysql"
  },


