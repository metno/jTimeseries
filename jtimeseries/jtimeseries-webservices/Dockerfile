FROM tomcat:7.0
MAINTAINER Met Norway <it-team-frontend@met.no>

# create snake oil certificate for testing
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -q update
RUN apt-get install -y -q apt-utils
RUN apt-get install -y -q ssl-cert
RUN make-ssl-cert generate-default-snakeoil

#clean tomcat
RUN ["rm", "-fr", "/usr/local/tomcat/webapps/ROOT", "/usr/local/tomcat/webapps/docs", "/usr/local/tomcat/webapps/examples", "/usr/local/tomcat/webapps/host-manager", "/usr/local/tomcat/webapps/manager"]

# install web app
ADD target/jtimeseries-webservices /usr/local/tomcat/webapps/jtimeseries-webservices

# install config
ENV JTIMESERIES_LOCAL_PROPERTIES /usr/local/tomcat/conf/jtimeseries.properties
ADD src/config/docker/jtimeseries.properties /usr/local/tomcat/conf/jtimeseries.properties
ADD src/config/docker/server.xml /usr/local/tomcat/conf/server.xml

# install extra fonts
ADD src/fonts /usr/lib/jvm/java-7-openjdk-amd64/jre/lib/fonts/

# expose port for TLS
EXPOSE 8443
