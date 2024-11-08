FROM maven:3.6-jdk-8-slim AS builder

# Install dependencies
RUN set -ex; \
  apt-get update; \
  apt-get -y install gpg libsnappy1v5 gettext-base libjemalloc-dev; \
  rm -rf /var/lib/apt/lists/*

COPY --chown=fluss:fluss build-target/ /opt/fluss/

 # Prepare environment
ENV FLUSS_HOME=/opt/fluss
ENV PATH=$FLUSS_HOME/bin:$PATH
RUN groupadd --system --gid=9999 fluss && \
     useradd --system --home-dir $FLUSS_HOME --uid=9999 --gid=fluss fluss
WORKDIR $FLUSS_HOME


# Configure container
COPY docker-entrypoint.sh /
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["help"]