# 规则埋点调用端开发手册

## 一、依赖管理
### 1、添加maven依赖
在具体的项目中引入，如ord-data-service项目pom中添加模块依赖
```
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-client</artifactId>
<version>${framework-core.version}</version>
</dependency>
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-storage-ctg</artifactId>
<version>${framework-core.version}</version>
</dependency>
```
### 2、添加配置
+ 添加分布式缓存配置(具体参考平台相关手册)

## 二、开发步骤
###（一）实现与CPC交互的相关接口
+ 接口名：com.shtel.bss.core.rule.service.IRlmRuleService
具体的实现内容，根据CPC的接口做适配。

###（二）实现因子接口
+ 接口名：com.shtel.bss.core.rule.runtime.IRuntimeFactorLoader
主要用于规则执行时，获取执行相关的因子信息，如staffId，orgId

###（三）规则埋点调用
#### (1) 调用方式一：静态方法调用
具体的方法详见：com.shtel.bss.core.rule.trigger.RuleTrigger
样例如下：
```
 TestObject1 testClassNameObject1 = new TestObject1();
        testClassNameObject1.setId(1L);
        TestObject2 testClassNameObject2 = new TestObject2();
        testClassNameObject2.setId(2L);
        RuleTrigger.classNameTrigger("validateClassName1", TestObject1.class.getName(),
                    testClassNameObject1, testClassNameObject2);
```
####（2）调用方式二：实体触发调用
+ 实体实现接口：com.shtel.bss.core.rule.entity.IMetaRuleEntity
样例如下：
```
TestObject1 testClassNameObject1 = new TestObject1();
        testClassNameObject1.setId(11L);
        TestObject2 testClassNameObject2 = new TestObject2();
        testClassNameObject2.setId(12L);
        testClassNameObject1.execute("validateRemote", testClassNameObject2);
```

+ 约束：
    + 该方式只能基于主数据调用，触发的规则数据，来源于主数据配置

###（四）JAVA类规则开发规范
####（1）单方法规则
```
public class TestSucess extends AbstractJavaCodeRuleExecutor {
    @Override
    public RuleResult execute(IRuleContext ruleContext, IRlmRule rule, RuleEvent ruleEvent) {
        System.out.println(Thread.currentThread().getName() + "testSuccess");
        return rule.createSuccessRuleResult("success", null);
    }
}

``` 
+ 要点：
    + 1、继承AbstractJavaCodeRuleExecutor
    + 2、返回结果为RuleResult
    
####（2）多方法规则
```
public class TestParallsWarn extends AbstractMultiJavaCodeRuleExecutor {
    public RuleResult testWarnParal(IRuleContext ruleContext, IRlmRule rule, TestObject1 object1) {
        System.out.println(Thread.currentThread().getName() + "TestWarn:" + object1);
        return rule.createErrorRuleResult("testWarnParalls",
            new String[] {"warn detal11.", "warnDetails12" });
    }
}
```
+ 要点：
    + 1、继承AbstractMultiJavaCodeRuleExecutor
    + 2、返回结果为RuleResult

####（3）返回规范
+ 规则返回值统一为：RuleResult
+ 分为四类：
    + SUCCESS：成功，不出现错误，不涉及数据变化
    + SILENCE：成功，涉及数据修改的。
    + WARN：提示类规则，用于提醒，如：订购xxx需要同时订购xxx
    + ERROR：异常类规则，主要用于校验，如：xxx 和 xxx可选包互斥。
    + CONFIRM：交互类规则：主要用于交互，如：需要客户确认，拆除移动语音同时拆除xxx？（目前没用）

###（五）规则执行屏蔽方法
    ```
    ERuleMode old = RuleModeConfig.getCurrentMode();
        try {
            RuleModeConfig.setRuleMode(ERuleMode.DISABLE);
            testClassNameObject1.execute("validateRemote", testClassNameObject2);
        } finally {
            RuleModeConfig.setRuleMode(old);
        }
    ```


##三、规则引擎对接
### 1、添加maven依赖
在Parent中增加规则引擎的版本
```
<dependency>
    <groupId>com.shtel.paas</groupId>
    <artifactId>PaasRule-SDK</artifactId>
    <version>1.4.0</version>
    <exclusions>
        <exclusion>
            <artifactId>maven-aether-provider</artifactId>
            <groupId>org.apache.maven</groupId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.apache.maven</groupId>
    <artifactId>maven-aether-provider</artifactId>
    <version>3.2.5</version>
</dependency>
```
特别注意：maven-aether-provider必须正确

在具体的项目中引入，如ord-data-service项目pom中添加模块依赖
```
<dependency>
<groupId>com.shtel.bss.core</groupId>
<artifactId>framework-core-rule-drools</artifactId>
<version>${framework-core.version}</version>
</dependency>
```
### 2、添加配置
+ 在系统环境配置中添加：
```
M2_HOME=/Users/linzhiqiang/dev/apache-maven-3.5.2-sh（可自定义）
```
**注意：**
在自己的系统变量中增加M2_HOME，M2_REPO的配置，具体的路径，可以使用自己的路径。
+ 在启动脚本或配置文件中，增加如下配置
```
--M2_REPO=/Users/linzhiqiang/dev/apache-maven-3.5.2-sh/repo（可自定义）
--paas.rule.kie.type=scanner  （默认配置不变）
--paas.rule.kieGroupId=com.shtel.paas  （加载规则drl项目的groupid）
--paas.rule.kieArtifactId=PaasRuleDrl   （加载规则drl项目的artifactId）
--paas.rule.kieVersion=LATEST  （默认配置不变）
--paas.rule.pool.coreSize=1000
--paas.rule.pool.maxSize=1000
--paas.rule.pool.queueSize=500
--paas.rule.logUrl=http://localhost:8001/rulesCallLog/add  (根据规则中心提供的地址)
--paas.rule.centorName=受理中心  （自定义）
```
### 3、规则受理返回类型
ruleType: DRL
className: sceneCode 场景编码
methodName: ruleCode 规则编码


