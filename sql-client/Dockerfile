FROM maven:3.6-jdk-8-slim AS builder

FROM apache/flink:1.18.1-scala_2.12

# Copy sql-client script
COPY bin/* /opt/sql-client/
RUN mkdir -p /opt/sql-client/lib

# Copy configuration
COPY conf/* /opt/flink/conf/

WORKDIR /opt/sql-client
ENV SQL_CLIENT_HOME=/opt/sql-client

COPY docker-entrypoint.sh /

COPY lib/* /opt/sql-client/lib/
COPY sql/* /opt/sql-client/sql/
COPY lib/* /opt/flink/lib/

RUN ["chmod", "+x", "/docker-entrypoint.sh"]
RUN ["chmod", "+x", "/opt/sql-client/sql-client"]
ENTRYPOINT ["/docker-entrypoint.sh"]