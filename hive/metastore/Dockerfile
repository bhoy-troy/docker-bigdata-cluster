FROM hive-base:1.0


COPY startup.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/startup.sh

EXPOSE 9083

HEALTHCHECK CMD netstat -tuplen | grep 9083 || exit 1

CMD startup.sh
