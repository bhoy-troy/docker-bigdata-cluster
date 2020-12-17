FROM  bigdata-baseimg:1.0

RUN apt update && apt install -y gpg-agent

RUN  curl https://downloads.apache.org/hadoop/common/KEYS | gpg --import

ENV HADOOP_VERSION 3.3.0
ENV HADOOP_URL https://downloads.apache.org/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz
ENV HADOOP_ASC https://downloads.apache.org/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz.asc
RUN set -x \
    && curl -fSL "${HADOOP_URL}" -o /tmp/hadoop.tar.gz \
    && curl -fSL "${HADOOP_ASC}" | gpg --verify  \
    && tar -xvf /tmp/hadoop.tar.gz -C /opt/ \
    && rm /tmp/hadoop.tar.gz*



RUN ln -s /opt/hadoop-${HADOOP_VERSION}/etc/hadoop /etc/hadoop
RUN cp /etc/hadoop/mapred-site.xml.template /etc/hadoop/mapred-site.xml

RUN mkdir /opt/hadoop-${HADOOP_VERSION}/logs
RUN mkdir /hadoop-data

ENV HADOOP_PREFIX=/opt/hadoop-${HADOOP_VERSION}
ENV HADOOP_CONF_DIR=/etc/hadoop
ENV MULTIHOMED_NETWORK=1
ENV USER=root
ENV PATH ${HADOOP_PREFIX}/bin/:${PATH}

ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
