# 规则埋点部署引用手册

## 一、依赖管理

### 1、添加maven依赖

在parent项目pom中添加规则模块依赖
```
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-client</artifactId>
<version>${framework-core.version}</version>
</dependency>
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-app</artifactId>
<version>${framework-core.version}</version>
</dependency>
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-storage-ctg</artifactId>
<version>${framework-core.version}</version>
</dependency>
```
## 二、构建规则中心
### 1、创建工程，添加依赖
在规则中心项目xx-rule-app项目pom中添加模块依赖
```
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-app</artifactId>
<version>${framework-core.version}</version>
</dependency>
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-storage-ctg</artifactId>
<version>${framework-core.version}</version>
</dependency>
```
### 2、修改配置文件，添加配置
+ 添加规则配置
```
framework.ruleService.isAllowRemote: false

```
+ 添加分布式缓存配置(具体参考平台相关手册)

