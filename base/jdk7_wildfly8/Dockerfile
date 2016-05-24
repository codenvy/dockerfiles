FROM codenvy/jdk7

RUN mkdir /home/user/wildfly && \
    wget \
    -qO- \
    "http://download.jboss.org/wildfly/8.2.0.Final/wildfly-8.2.0.Final.tar.gz" | tar -zx --strip-components=1 -C /home/user/wildfly/
RUN cd /home/user/wildfly/standalone/configuration/ && \
    sed -i 's/enable-welcome-root="true"/enable-welcome-root="false"/g' standalone.xml && \
    sed -i 's/127.0.0.1/0.0.0.0/g' standalone.xml && \
    sed -i 's/<deployment-scanner/<deployment-scanner auto-deploy-exploded="true"/g' standalone.xml

EXPOSE 8080
ENV CODENVY_APP_PORT_8080_HTTP 8080

WORKDIR /home/user/wildfly/bin/

CMD ./standalone.sh

# ===== Usage =====
# FROM codenvy/jdk7_wildfly8
# ADD $app$ /home/user/wildfly/standalone/deployments/ROOT.war
# ===== OR (debug) =====
# FROM codenvy/jdk7_wildfly8
# EXPOSE 8000
# ENV CODENVY_APP_PORT_8000_DEBUG 8000
# ENV JAVA_OPTS "-Xdebug -Xnoagent -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
# ADD $app$ /home/user/wildfly/standalone/deployments/ROOT.war
