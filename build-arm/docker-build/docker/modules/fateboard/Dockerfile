FROM openjdk:8u342-jre as builder
WORKDIR /data/projects/fate/
COPY fateboard.tar.gz .
RUN tar -xzf fateboard.tar.gz

FROM openjdk:8u342-jre

RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

ENV TZ="Asia/Shanghai"

WORKDIR /data/projects/fate/fateboard/

COPY --from=builder /data/projects/fate/fateboard /data/projects/fate/fateboard
EXPOSE 8080

CMD java -Dspring.config.location=/data/projects/fate/fateboard/conf/application.properties  -Dssh_config_file=/data/projects/fate/fateboard/conf  -Xmx2048m -Xms2048m -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:gc.log -XX:+HeapDumpOnOutOfMemoryError  -jar fateboard.jar
