# 0.0.1-SNAPSHOT
## 2018-08-30
* 更新BaseDao，移除updateSelective相关的方法，禁止直接使用该方法。

## 2018-09-04 
* 修改BaseMapper.queryAttrs方法，入参由Entity改为Map。
* 增加queryAttr参数转换时的过滤功能。

## 2018-09-10
* 主数据类中增加对AttrValueId字段的处理。
* 注意：本次修改会产生应用报错，相关的Attr对象需要实现接口 getSlaAttrValueId

## 2018-09-19
* 在AbstractBaseFacadeImpl增加getRestTemplate的方法，
* 在AbstractBaseFacadeImpl增加isExternal

## 2018-9-29
* 增加全局索引相关API

## 2018-10-12
* 增加规则引擎相关的内容支持。

## 2018-10-18
* IBusiObjAttr增加方法。
## 2018-10-26
* 引入规则引擎相关的包，完成规则引擎对接包装。
## 2018-11-13
* BaseEntity增加HashCode方法


