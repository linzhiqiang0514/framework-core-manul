
# FRAMEWOKR-CORE工程简介

## 工程结构说明

* framework-core：工程父pom，继承于SHTEL-PAAS-PARENT，用于声明工程范围内的maven定义
  * framework-core-base：主要包含一些基本的工具类，如StringUtils、NumberUtils等。
  * framework-core-pub：主要包含一些数据层和业务层共享的类，如ApplicationContextUtils，PageInfo，Entity的Base接口等。
    - framework-core-data-common：数据层模块目录
      - framework-core-data-common-service，主要包含数据层操作的基类，接口等，如BaseEntity，BaseService，BaseDao,BaseMapper。
      - framework-core-data-common-app：主要包含数据服务暴露的基类，DTO转换的基类，如BaseControl，BaseEntityMapper（mapstruct）。
    - framework-core-biz-common：业务层模块目录
      - framework-core-biz-common-service，主要包含业务层操作的BO基类，接口等，如BaseEntityBO，BaseBOService。
      - framework-core-biz-common-app：主要包含业务服务暴露的基类，DTO转换的基类，如BaseBizControl，BaseEntityMapper（mapstruct）。
  * framework-core-pub-api：主要包含一些数据和业务API层共享的类，如BaseDTO，BaseFacade的接口等。
    - framework-core-data-common-api：数据层API模块目录
      - framework-core-data-common-api-intf：主要包含数据层API操作的基类，接口等，如BaseDTO，BaseFacade。
      - framework-core-data-common-api-impl：主要包含数据层API的实现，如BaseFacadeImpl。
    - framework-core-biz-common-api：业务层API模块目录
      - framework-core-biz-common-api-intf：主要包含业务层API操作的基类，接口等，如BaseDTO，BaseFacade。
      - framework-core-biz-common-api-impl：主要包含业务服务层API的实现，如BaseFacadeImpl。
  * framework-core-components：主要包含基于commons的一些扩展，如主数据，DDD模式的扩展。
    - framework-core-meta：基于主数据的扩展
      - framework-core-meta-pub：主要包含主数据基础类，扩展的基础类，如IMetaEntity，主数据相关的获取类，如BusiObjProvider。
      - framework-core-meta-data-service：主要包含基于主数据模式的数据层扩展。
      - framework-core-meta-biz-service：主要包含基于主数据的业务层扩展。
    - framework-core-ddd：基于ddd的扩展
      - framework-core-ddd-pub：主要包含ddd扩展的基础类，如IDomBaseEntity,IDomRepository，主数据相关的获取类。
      - framework-core-ddd-data-service：主要包含基于ddd模式的数据层扩展。
      - framework-core-ddd-biz-service：主要包含基于ddd的业务层扩展。




