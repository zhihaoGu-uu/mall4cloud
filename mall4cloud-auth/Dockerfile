# 该镜像需要依赖的基础镜像
FROM openjdk:17-jdk-alpine

# 安装 ttf-dejavu 字体和 fontconfig 库，以解决 NoClassDefFoundError: X11FontManager 错误
RUN apk update && \
    apk add --no-cache ttf-dejavu fontconfig

RUN mkdir -p /mall4cloud/mall4cloud-auth

WORKDIR /mall4cloud/mall4cloud-auth

# 声明服务运行在9101端口
EXPOSE 9101
# 将当前目录下的jar包复制到docker容器的/目录下
ADD ./target/mall4cloud-auth.jar ./mall4cloud-auth.jar
# 指定临时文件目录
VOLUME /tmp
# 项目配置的日志文件目录
#VOLUME /logs
# 指定docker容器启动时运行jar包
# 使用 G1GC，让 JVM 自动感知容器的内存限制
# 使用 -XX:MaxRAMPercentage=N 设置最大内存占容器限制的百分比
ENTRYPOINT ["java","-jar","-Djava.awt.headless=true","-Dspring.cloud.nacos.discovery.ip=192.168.159.131", "-XX:+UseG1GC","-XX:MaxRAMPercentage=9.0","mall4cloud-auth.jar"]
# 指定时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 指定维护者的名字
MAINTAINER gzh