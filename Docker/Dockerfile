# Docker image for springboot application
# VERSION 0.0.1
# Author: lx

### 基础镜像
FROM java:8

#作者
MAINTAINER lx <1195423292@qq.com>

#系统编码
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

#声明一个挂载点，容器内此路径会对应宿主机的某个文件夹
VOLUME /tmp

#暴露8080端口
EXPOSE 8080

#镜像时区
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

#定义参数
RUN bash -c 'touch /app.jar'

#应用构建成功后的jar文件被复制到镜像内，名字也改成了app.jar
ADD eladmin-system-2.3.jar app.jar

#启动容器时的进程
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Dfile.encoding=UTF8","-Duser.timezone=GMT+08","-jar","app.jar"]
