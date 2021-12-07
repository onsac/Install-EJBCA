<h3 align="center">OnSAC</h3>

<p align="center">
  Automações e Integrações sem limitações (AIops/DEVops)
  <br>
  <a href="https://onsac.com/"><strong>Conheça mais sobre nosso serviço »</strong></a>
  </p>
  
  
## Install-EJBCA

Manual de instalação do EJBCA

```sh
yum install vim ntp ntpdate epel-release wget tar unzip java-1.8.0-openjdk-devel ant psmisc mariadb bc patch
```
```sh
yum install htop
```
```sh
yum update install
```
```sh
stop firewall-cmd
```
```sh
yum install mariadb-server
```
```sh
sudo systemctl enable mariadb
```
```sh
sudo systemctl start mariadb
```
```sh
sudo systemctl status mariadb
```
```sh
sudo mysql_secure_installation
 > password and all Y
 ```
 ```sh
mysql -u root -p
```
```sh
CREATE DATABASE ejbca CHARACTER SET utf8 COLLATE utf8_general_ci;
```
```sh
GRANT ALL PRIVILEGES ON ejbca.* TO 'ejbca'@'localhost' IDENTIFIED BY 'ejbca';
```
```sh
quit
```
```sh
cd /tmp
```
```sh
wget https://download.jboss.org/wildfly/10.1.0.Final/wildfly-10.1.0.Final.tar.gz
```
```sh
sudo groupadd -r wildfly
```
```sh
sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly
```
```sh
sudo tar -zxf wildfly-10.1.0.Final.tar.gz -C /opt/
```
```sh
sudo ln -s /opt/wildfly-10.1.0.Final /opt/wildfly
```
```sh
cd /opt
```
```sh
ls
```
```sh
sudo chown -RH wildfly: /opt/wildfly
```
```sh
sudo mkdir -p /etc/wildfly
```
```sh
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/
```
```sh
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/
```
```sh
sudo sh -c 'chmod +x /opt/wildfly/bin/*.sh'
```
```sh
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/
```
```sh
vi /opt/wildfly/bin/standalone.conf 
```
```sh
> JAVA_OPTS="-Xms2048m -Xmx2048m -Djava.net.preferIPv4Stack=true"
```
```sh
sudo systemctl deamon-reload
```
```sh
sudo systemctl enable wildfly
```
```sh
sudo systemctl start wildfly
```
```sh
reboot
```
```sh
http:192.168.1?:8080
```
```sh
sudo -s
```
```sh
cd /tmp
```
```sh
wget https://downloads.mariadb.com/Connectors/java/connector-java-2.2.6/mariadb-java-client-2.2.6.jar
```
```sh
sudo -u wildfly cp /tmp/mariadb-java-client-2.2.6.jar /opt/wildfly/standalone/deployments/mariadb-java-client.jar
```
```sh
cd /opt/wildfly/bin
```







