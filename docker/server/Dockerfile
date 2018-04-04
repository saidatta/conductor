#
# conductor:server - Netflix conductor server
#
FROM ubuntu

MAINTAINER Netflix OSS <conductor@netflix.com>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get clean

RUN apt-get install -y iputils-ping

RUN apt-get install -y curl

# Make app folders
RUN mkdir -p /app/config /app/logs /app/libs

# Copy the project directly onto the image
COPY ./docker/server/bin /app
COPY ./docker/server/config /app/config
COPY ./server/build/libs/conductor-server-*-all.jar /app/libs

# Setup Volume
VOLUME ["/app/config/config.properties"]

# Copy the files for the server into the app folders
RUN chmod +x /app/startup.sh

EXPOSE 8080

CMD [ "/app/startup.sh" ]
ENTRYPOINT [ "/bin/bash"]
