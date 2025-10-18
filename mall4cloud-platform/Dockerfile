# 该镜像需要依赖的基础镜像
FROM openjdk:17-jdk-alpine

RUN mkdir -p /mall4cloud/mall4cloud-platform

WORKDIR /mall4cloud/mall4cloud-platform

# 声明服务运行在9112端口
EXPOSE 9112
# 将当前目录下的jar包复制到docker容器的/目录下
ADD ./target/mall4cloud-platform.jar ./mall4cloud-platform.jar
# 指定临时文件目录
VOLUME /tmp
# 项目配置的日志文件目录
#VOLUME /logs
# 指定docker容器启动时运行jar包
ENTRYPOINT ["java","-jar","-Dspring.cloud.nacos.discovery.ip=192.168.159.131","-XX:+UseG1GC","-XX:MaxRAMPercentage=9.0","mall4cloud-platform.jar"]
# 指定时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 指定维护者的名字
MAINTAINER gzh