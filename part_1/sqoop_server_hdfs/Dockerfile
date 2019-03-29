FROM dvoros/hadoop:3.1.0

USER root

ENV SQOOP_HOME /usr/local/sqoop
ENV MYSQL_JAR_VERSION=5.1.46

RUN yum install zip unzip -y
RUN curl -s https://www.apache.org/dist/sqoop/1.4.7/sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz | tar -xz -C /usr/local
RUN ln -s /usr/local/sqoop-1.4.7.bin__hadoop-2.6.0 $SQOOP_HOME

RUN mkdir -p /tmp/jdbc \
    && curl -Lo /tmp/mysql-connector-java-$MYSQL_JAR_VERSION.tar.gz https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-$MYSQL_JAR_VERSION.tar.gz \
    && tar -xvf /tmp/mysql-connector-java-$MYSQL_JAR_VERSION.tar.gz -C /tmp/jdbc \
    && rm /tmp/mysql-connector-java-$MYSQL_JAR_VERSION.tar.gz \
    && mv /tmp/jdbc/mysql-connector-java-$MYSQL_JAR_VERSION/mysql-connector-java-$MYSQL_JAR_VERSION-bin.jar $SQOOP_HOME/lib/ \
    && rm -rf /tmp/mysql-connector-java-$MYSQL_JAR_VERSION/

ENV PATH $PATH:$HADOOP_HOME/bin:$SQOOP_HOME/bin

COPY bootstrap.sh /etc/bootstrap.sh
RUN chown root.root /etc/bootstrap.sh
RUN chmod 700 /etc/bootstrap.sh

CMD ["/etc/bootstrap.sh"]
