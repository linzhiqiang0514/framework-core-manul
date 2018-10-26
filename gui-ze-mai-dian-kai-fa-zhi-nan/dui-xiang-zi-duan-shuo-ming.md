# 对象字段说明

## CPC返回RULE对象说明
IRlmRule接口：
```
    Long getId();
    String getMethodName();
    String getRuleType();
    String getRuleExecuteClass();
    boolean isRemoteRule();
    boolean isParallelsRule();
    boolean isLocalRule();
    int getGroupSeq();
```

id：主键
methodName：规则执行类的方法，或规则引擎的规则编码，可空。
ruleType：目前可选值：JVA，java类规则；DRL，规则引擎规则。
ruleExecuteClass：规则执行类，或规则引擎的场景编码
isRemoteRule：标记规则是否需要远程执行
isParallelsRule：标记规则是否可以并行
isLocalRule：标记是否本地执行规则
groupSeq：规则分组的标识，整形。


