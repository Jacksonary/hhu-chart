# Chart包结构说明

1. 推荐chart包名字做成`<项目组-项目名-project>`的样式，比如这里的`hhu-project`；
2. 目录`hhu-project`中`templates`目录、`Chart.yaml`、`values.yaml`已经是一个完整的chart包，所有数据由`valuses.yaml`提供，如果需要根据不同的服务定制参数，在`templates`同级目录下面创建额外的配置文件，比如这里的`server-account`等，它会覆盖本身应用中的`values.yaml`属性值；
3. 该chart结构相对比较完整，也是目前调式完给项目组使用的模板


---
注：其中对应的`Dockerfile`如下：

```dockerfile
FROM registry.cn-shanghai.aliyuncs.com/xxxx/centos7-jdk8:xx
LABEL "project"="hhu-server"
LABEL "server-name"="server-task"
RUN mkdir -p /data/service
WORKDIR /data/service
COPY  server-task/target/server-task.jar .
CMD java $JAVA_OPTS -Dspring.profiles.active=$SPRING_ENV -Denv=$APOLLO_ENV -Dapollo.configService=$APOLLO_CONFIG_SERVICE -Dserver.port=8080 $REMOTE_DEBUG_ARGS -jar server-task.jar
```
