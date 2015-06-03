FROM codenvy/jdk7

ENV HOME /home/user
ENV CLI_VERSION 2.10.0 
ENV CLI_HOME /opt/codenvy-cli-$CLI_VERSION
ENV CLI_BIN_URL http://maven.codenvycorp.com/content/repositories/public/com/codenvy/cli/cli-assembly/$CLI_VERSION/cli-assembly-$CLI_VERSION.tar.gz
ENV PATH $CLI_HOME/bin:$PATH 
RUN wget -qO- $CLI_BIN_URL | sudo tar zx -C /opt/ && \
echo "export CLI_HOME=$CLI_HOME" >> $HOME/.bashrc && \
echo "export PATH=$PATH" >> $HOME/.bashrc && \
sudo chown user:user -R $CLI_HOME && \

CMD sleep 4h
