#任务操作接口

##创建任务接口

###功能说明：

通过此接口可以创建新的任务

###更新说明：

创建任务,支持使用多个无主叫固话,只需设置总并发数,由系统自动分配每个线路的并发。

>入参JSON实例：

```
{
    "companyId" : 1, 
    "taskName" : "测试任务", 
    "taskType" : 2, 
    "startDate" : "2017-10-19",
    "workingStartTime" : "08:00",
    "workingEndTime" : "22:00", 
    "breakStartTime" :"12:00",
    "breakEndTime" : "13:00",
    "userPhoneIds" : [1], 
    "callType" : 0, 
    "concurrencyQuota" : 1, 
    "robotDefId" : 1, 
    "sceneDefId" : 1, 
    "sceneRecordId" : 7, 
    "concurrencyQuota":1,
    "smsType":1,
    "remark" : "创建任务" 
}
```

>JSON响应实例：

```
{
    "code": 200,
    "data": 67,
    "resultMsg": "操作成功",
    "errorStackTrace": null
}

```

###请求：

URL：http://api.byrobot.cn/openapi/v1/task/createTask

###请求方法：

POST


###请求参数:

参数名 | 类型 | 是否必须 | 描述 | 实例 
--------- | ------- |------- | ------ |----------
 companyId| Integer| 是 | 公司Id| 1 |
 taskName| String| 是 |任务名称| 测试API任务 |
 taskType| Integer| 是 | 任务类型, 1-定时,2-手动| 1 |
 startDate| String| 是 | 任务开始日期| "2017-10-19"  |
 workingStartTime| String| 否 | 可拨打开始时间| 08:00 |
 workingEndTime| String| 否 | 可拨打结束时间| 22:00 |
 breakStartTime| String| 否 | 暂时停止开始时间| 12:00 |
 breakEndTime| String| 否 | 暂时停止结束时间| 13:00 |
 userPhoneIds| Integer| 是 | 主叫电话号码id列表，详见获取公司的主叫电话列表(getPhones)接口| [1,2] |
 sceneDefId| Integer| 是 | 场景id| 1 |
 robotDefId| Integer| 是 | 机器人id| 1 |
 sceneRecordId| Integer| 是 | 机器人话术录音id| 1 |
 callType| Integer| 否 | 外呼类型，0-sim卡,1-固话（默认）, 2-无主叫| 1 |
 concurrencyQuota| Integer| 否 | 并发数，默认1| 1 |
 smsType| Integer| 否 | 是否发送短信：1-是，0-否（默认）| 1 |
 remark| String| 否 | 备注| 测试|



###响应：

参数名 | 类型 | 描述 
--------- | ------- |------
 code|integer | 响应码 |
 resultMsg| String | 响应说明 |

##启动任务接口

###功能说明：

通过此接口可以启动指定的任务

>JSON响应实例：

```
{
    "code": 200,
    "data": null,
    "resultMsg": "启动成功",
    "errorStackTrace": null
}

```

###请求：

URL：http://api.byrobot.cn/openapi/v1/task/start

###请求方法：

POST


###请求参数:

参数名 | 类型 | 是否必须 | 描述 | 实例 
--------- | ------- |------- | ------ |----------
 taskId| Integer| 是 | 任务Id| 1 |


###响应：

参数名 | 类型 | 描述 
--------- | ------- |------
 code|integer | 响应码 |
 resultMsg| String | 响应说明 |
 
##暂停任务接口
 
###功能说明：
 
 通过此接口可以暂停指定的任务
 
 >JSON响应实例：
 
 ```
 {
     "code": 200,
     "data": null,
     "resultMsg": "执行成功",
     "errorStackTrace": null
 }
 
 ```
 
###请求：
 
 URL：http://api.byrobot.cn/openapi/v1/task/pause
 
###请求方法：
 
 POST
 
 
###请求参数:
 
 参数名 | 类型 | 是否必须 | 描述 | 实例 
 --------- | ------- |------- | ------ |----------
  taskId| Integer| 是 | 任务Id| 1 |
 
 
###响应：
 
 参数名 | 类型 | 描述 
 --------- | ------- |------
  code|integer | 响应码 |
  resultMsg| String | 响应说明 |

##停止任务接口
 
###功能说明：
 
 通过此接口可以停止  指定的任务
 
 >JSON响应实例：
 
 ```
 {
     "code": 200,
     "data": null,
     "resultMsg": "执行成功",
     "errorStackTrace": null
 }
 
 ```
 
###请求：
 
 URL：http://api.byrobot.cn/openapi/v1/task/stop
 
###请求方法：
 
 POST
 
 
###请求参数:
 
 参数名 | 类型 | 是否必须 | 描述 | 实例 
 --------- | ------- |------- | ------ |----------
  taskId| Integer| 是 | 任务Id| 1 |
 
 
###响应：
 
 参数名 | 类型 | 描述 
 --------- | ------- |------
  code|integer | 响应码 |
  resultMsg| String | 响应说明 |

##向任务中导入客户接口
 
###功能说明：
 
 通过此接口可以向指定的任务导入客户信息，用于拨打电话
 
 >入参JSON实例:
 
  ```
 
{
	"taskId":10000,
	"companyId":2000,
	"customerInfoList":[
		{
			"name":"测试0",
			"phone":"18311110000",
			"properties":{  //客户额外信息，如果话术中包含变量，则需要在properties中加上对应字段，map的key和话术中的变量保持一致。如果话术没有变量，则不要properties
				"real_name":"real"
			}
		},
		{
			"name":"测试1",
			"phone":"18311112222",
			"properties":{  //客户额外信息，如果话术中包含变量，则需要在properties中加上对应字段，map的key和话术中的变量保持一致。如果话术没有变量，则不要properties
				"real_name":"real"
			}
		}
	]
} 
  
  ```
  
 >JSON响应实例：
 
 ```
 {
     "code": 200,
     "data": null,
     "resultMsg": "操作成功",
     "errorStackTrace": null
 }
 
 ```
 
###请求：
 
 URL：http://api.byrobot.cn/openapi/v1/task/importTaskCustomer

###请求方法：
 
 POST
 
 
###请求参数:
 
 参数名 | 类型 | 是否必须 | 描述 | 实例 
 --------- | ------- |------- | ------ |----------
  companyId| Integer| 是 | 公司id| 1 |
  taskId| Integer| 是 | 任务Id| 1 |
  name| String| 是 | 客户名称| 张三 |
  phone| String| 是 | 客户电话| 13998987676 |
  properties| Map<String,String>| 否 | 客户额外信息| 请看json入参 |

 
 
###响应：
 
 参数名 | 类型 | 描述 
 --------- | ------- |------
  code|integer | 响应码 |
  resultMsg| String | 响应说明 |
