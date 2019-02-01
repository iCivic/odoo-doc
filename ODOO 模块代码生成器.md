代码生成器
================

*   [1. 模块](#module)
    *   [1.1 概要](#overview)
    *   [1.2 角色](#roles)
    *   [1.3 路由](#routes)
    *   [1.4 数据字典](#dictionary)
    *   [1.5 定时行为](#scheduletask)
    *   [1.6 事件行为](#autotask)
*   [2. 模型](#models)
    *   [2.1 项目](#project)
    *   [2.2 项目代码生成任务](#auto_code_job)
    *   [2.3 项目代码任务向导](#auto_code_job_wizard)
    *   [2.4 项目数据字典](#dictionary)
    *   [2.5 项目数据字典列表](#dictionary_value)
    *   [2.6 分模块](#module)
    *   [2.7 分模块路由](#route)
    *   [2.8 分模块角色](#role)
    *   [2.9 分模块模型](#model)
    *   [2.10 模型字段](#field)
    *   [2.11 模型用例](#usecase)
    *   [2.12 数据字典](#standard_option)
    *   [2.13 数据字典选项值](#standard_option_value)
    *   [2.14 第三方模块](#thirdy_module)
    *   [2.15 代码模板](#code_template)
*   [用例](#usecases)
* * *

<h2 id="module">1. 模块</h2>

<h3 id="overview">1.1 概要</h3> 


名称 | 值 | 描述
---|---|---
模块代码 | idu_auto_coder | 
模型前缀 |  idu_coder_ | 
模块名称 |  代码生成器 | 
模块图标 |  | 
版本 |  | 
模块描述摘要 |  | 
模块描述 |  | 
模块依赖项 |  | 
外部包依赖项 | "python": [], "bin": [] | 
是否基础模块 |  |
是否可安装 |  |
是否应用程序 |  |
是否自动安装 |  |
安装前钩子 |  |
安装后钩子 |  |
卸载后钩子 |  |

<h3 id="roles">1.2 角色</h3> 

角色名称 | 角色代码 | 角色概要描述 | 查权限 | 改权限 | 增权限 | 删权限
---|---|---|---|---|---|---
系统设计师| systems_analyst| 主要负责模型配置| 是| 是| 是| 是
系统管理员| systems_analyst| system_administrator| 是| 是| 是| 是

<h3 id="roles">1.3 路由</h3> 

- 下载Excel文件

```
    @http.route([
    "/idu/autocoder/module/excel/<int:moduleId>"
    ], auth="public", methods=["GET"], csrf=False, type="http")
    def generateExcel(self, moduleId, **kw):
```



```
sequenceDiagram
A->>B: How are you?
B->>A: Great!
```



```seq
title  上级指令管理 - 参考类指令的一般流程

autonumber

participant 省情报平台
participant 市情报平台
actor 市反恐支队
actor 区县派出所

市情报平台->省情报平台: 定期轮询某类核查任务指令
省情报平台 -->市情报平台: 返回某类核查任务列表
市情报平台 ->市情报平台: 更新某类核查任务
市情报平台 ->省情报平台: 更新任务签收状态
```

- 生成代码

``` 
    @http.route([
        "/idu/autocoder/module/code/<int:jobId>"
    ], auth="public", methods=["GET"], csrf=False, type="http")
    def generateSourceCode(self, jobId, **kw):
```


<h3 id="dictionary">数据字典</h3> 

<h3 id="scheduletask">定时行为</h3> 

<h3 id="autotask">事件行为</h3> 





