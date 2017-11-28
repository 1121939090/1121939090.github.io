---
layout:     post
title:      "ThinkPHP函数详解：C方法"
subtitle:   "ThinkPHP函数详解：C方法"
date:       2017-11-28 13:00:00
author:     "Lzy"
header-img: "img/post-bg-thinkphp.jpg"
tags:
    - ThinkPHP
---
C方法是ThinkPHP用于设置、获取，以及保存配置config文件中参数的方法，使用频率较高。
了解C方法需要首先了解下ThinkPHP的配置，因为C方法的所有操作都是围绕配置相关的。ThinkPHP的配置文件采用PHP数组格式定义。  
由于采用了函数重载设计，所以用法较多，我们来一一说明下。  
**设置参数**  

```
C('DB_NAME','thinkphp');
```  
表示设置DB_NAME配置参数的值为thinkphp，由于配置参数不区分大小写，所以下面的写法也是一样：  

```
C('db_name','thinkphp');
```  
但是建议保持统一大写的配置定义规范。  
项目的所有参数在未生效之前都可以通过该方法动态改变配置，最后设置的值会覆盖前面设置或者惯例配置里面的定义，也可以使用参数配置方法添加新的配置。  
支持二级配置参数的设置，例如：  

```
C('USER.USER_ID',8);
```  
配置参数不建议超过二级。
如果要设置多个参数，可以使用批量设置，例如：
```
$config['user_id'] = 1;
$config['user_type'] = 1;
C($config);
```  
如果C方法的第一个参数传入数组，就表示批量赋值，上面的赋值相当于：  

```
C('USER_ID',1);
C('USER_TYPE',1);
```
**获取参数**  
要获取设置的参数，可以用：  

```
$userId = C('USER_ID');
$userType = C('USER_TYPE');
```  
如果USER_ID参数尚未定义过，则返回NULL。
也可以支持获取二级配置参数，例如：  

```
$userId = C('USER.USER_ID');
```  
如果传入的配置参数为空，表示获取全部的参数：  

```
$config = C();
```  
**保存设置**  
3.1版本增加了一个永久保存设置参数的功能，仅针对批量赋值的情况，例如：  

```
$config['user_id'] = 1;
$config['user_type'] = 1;
C($config,'name');
```  
在批量设置了config参数后，会连同当前所有的配置参数保存到缓存文件（或者其他配置的缓存方式）。
保存之后，如果要取回保存的参数，可以用  

```
$config = C('','name');
```  
其中name就是前面保存参数时用的缓存的标识，必须一致才能正确取回保存的参数。取回的参数会和当前的配置参数合并，无需手动合并。








