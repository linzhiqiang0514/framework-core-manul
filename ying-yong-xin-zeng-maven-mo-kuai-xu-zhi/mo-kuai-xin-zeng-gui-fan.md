# Maven模块新增规范
## 普通Jar包模块
### 定义Plugin信息
```
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
            </plugin>

            <!-- resource插件 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
            </plugin>

            <!-- jar打包相关插件 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
            </plugin>


            <plugin>
                <artifactId>maven-source-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>com.google.code.maven-replacer-plugin</groupId>
                <artifactId>replacer</artifactId>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>buildnumber-maven-plugin</artifactId>
            </plugin>

        </plugins>
    </build>
```
### 添加Version.txt.template文件
在模块根目录添加文件 Version.txt.template，内容如下：
> 时间  @buildtime@
BUILD   @buildnumber@
MAVEN @pomversion@

[Version.txt.template](../.gitbook/assets/Version.txt.template)


## Spring-boot可运行jar
### 增加plugin信息
```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>unpack</id>
                        <phase>generate-resources</phase>
                        <goals>
                            <goal>unpack</goal>
                        </goals>
                        <configuration>
                            <artifactItems>
                                <artifactItem>
                                    <groupId>com.shtel.paas</groupId>
                                    <artifactId>shtel-paas-sdk</artifactId>
                                    <version>${paas-sdk.version}</version>
                                    <type>jar</type>
                                    <outputDirectory>${project.build.directory}</outputDirectory>
                                    <includes>Application/**</includes>
                                </artifactItem>
                            </artifactItems>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-assembly-plugin</artifactId>
                <executions>
                    <execution>
                        <id>paaspkg</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <descriptors>
                                <descriptor>target/Application/assembly.xml</descriptor>
                            </descriptors>
                            <attach>false</attach>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```


