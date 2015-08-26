FROM codenvy/jdk7

ENV DEBIAN_FRONTEND noninteractive

# Install and setup MySQL
RUN sudo apt-get update && \
    sudo apt-get install pwgen && \
    sudo -E bash -c "apt-get -y --no-install-recommends install mysql-server" && \
    sudo sed -i.bak 's/127.0.0.1/0.0.0.0/g' /etc/mysql/my.cnf && \
    sudo service mysql restart && \
    sudo mysql -uroot -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'; FLUSH PRIVILEGES;"

# Create MySQL user and database
RUN sudo service mysql restart && \
    CODENVY_MYSQL_PASSWORD=$(pwgen -N 1) && \
    CODENVY_MYSQL_DB=testdb_$(pwgen -N 1) && \
    CODENVY_MYSQL_USER=codenvy && \
    echo "export CODENVY_MYSQL_PASSWORD=$CODENVY_MYSQL_PASSWORD" >> /home/user/.mysqlrc && \
    echo "export CODENVY_MYSQL_USER=$CODENVY_MYSQL_USER" >> /home/user/.mysqlrc && \
    echo "export CODENVY_MYSQL_DB=$CODENVY_MYSQL_DB" >> /home/user/.mysqlrc && \
    sudo mysql -uroot -e "CREATE USER '$CODENVY_MYSQL_USER'@'%' IDENTIFIED BY '"$CODENVY_MYSQL_PASSWORD"'" && \
    sudo mysql -uroot -e "GRANT ALL PRIVILEGES ON *.* TO '$CODENVY_MYSQL_USER'@'%' IDENTIFIED BY '"$CODENVY_MYSQL_PASSWORD"'; FLUSH PRIVILEGES;" && \
    sudo mysql -uroot -e "CREATE DATABASE $CODENVY_MYSQL_DB;"

ADD startup.sh /home/user/startup.sh

RUN sudo chmod +x /home/user/startup.sh

EXPOSE 3306

CMD sudo /home/user/startup.sh