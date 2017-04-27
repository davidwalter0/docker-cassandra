# Spotify Cassandra 2.0 Base Image
#
# VERSION               0.1
#
# Installs Cassandra 2.0 package. Does only basic configuration.
# Tokens and seed nodes should be configured by child images.

FROM java:openjdk-8-jre

ENV DEBIAN_FRONTEND noninteractive

# Add DataStax sources
# RUN curl -L http://debian.datastax.com/debian/repo_key | apt-key add -
# RUN echo "deb http://debian.datastax.com/community stable main" > /etc/apt/sources.list.d/datastax.list
# RUN curl https://www.apache.org/dist/cassandra/KEYS | apt-key add -
# RUN echo "deb http://www.apache.org/dist/cassandra/debian 36x main" | tee -a /etc/apt/sources.list.d/cassandra.sources.list
# Workaround for https://github.com/docker/docker/issues/6345
# RUN ln -s -f /bin/true /usr/bin/chfn && \
#     apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA && \
#     echo "deb http://debian.datastax.com/community stable main" | \
#     tee -a /etc/apt/sources.list.d/cassandra.sources.list && \
#     curl -L https://debian.datastax.com/debian/repo_key | apt-key add -

RUN ln -s -f /bin/true /usr/bin/chfn && \
    apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA && \
    echo "deb http://www.apache.org/dist/cassandra/debian 310x main" | tee -a /etc/apt/sources.list.d/cassandra.sources.list && \
    curl https://www.apache.org/dist/cassandra/KEYS | apt-key add - && \
    apt-get update && \
    apt-get install -y cassandra-tools


# RUN add-apt-repository ppa:openjdk-r/ppa && \
#     apt-get update && \
#     apt-get install openjdk-8-jdk && \
#     update-alternatives --config java 

# Install Cassandra 2.0.10
#   apt-get install -y cassandra=2.0.10 dsc20=2.0.10-1 && \

#  rm -rf /var/lib/apt/lists/*

ENV CASSANDRA_CONFIG /etc/cassandra

# Run base config script
ADD scripts/config-cassandra-base.sh /usr/local/bin/config-cassandra-base
RUN /usr/local/bin/config-cassandra-base

# Necessary since cassandra is trying to override the system limitations
# See https://groups.google.com/forum/#!msg/docker-dev/8TM_jLGpRKU/dewIQhcs7oAJ
RUN rm -f /etc/security/limits.d/cassandra.conf

EXPOSE 7199 7000 7001 9160 9042 22 8012 61621

CMD [""]
