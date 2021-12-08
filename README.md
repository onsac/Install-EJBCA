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
firewall-cmd --state
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
sudo systemctl daemon-reload
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
http:192.168.1:8080
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
```sh
./jboss-cli.sh -c
>data-source add --name="ejbcads" --driver-name="mariadb-java-client.jar" --connection-url="jdbc:mysql://127.0.0.1:3306/ejbca" --jndi-name="Java:/EJbcaDS" --use-ccm=true --driver-class="org.maiadb.jdbc.Driver" --user-name="ejbca" --password="ejbca" --validate-on-match=true --background-validation=false --prepared-statements-cache-size=50 --share-prepared-statements=true --min-pool-size=5 --max-pool-size=150 --pool-prefill=true --transaction-isolation=TRANSACTION_READ_COMMITTED --check-valid-connection-sql="select 1;"
```
```sh
>:reload
```
```sh
>quit
```
```sh
Download EJBCA
```
```sh
cd /tmp
```
```sh
mv ejbca_ce_7_4_0.zip /opt
```
```sh
ls 
```
```sh
rm wildfly-10.1.0.Final.tar.gz 
   remove regular file 'wildfly-10.1.0.final.tar.gz´? y
```
```sh
rm mariadb-java-client-2.2.6.jar
   remove regular file `mariadb-java-client-2.2.6.jar´?y
```
```sh
cd /opt
```
```sh
sudo unzip ejbca_ce_7_4_0. zip
```
```sh
rm ejbca_ce_7_4_0.zip
   remove regular file `ejbca_ce_7_4_0.zip´ ? y
```
```sh
>: # ls 
```
```sh
>: # cd ejbca_ce_7_4_0/
ejbca_ce_7_4_0] # cd conf
```
```sh
>: vi database.properties
```
```sh
>:wq!
```
```sh
>: vi cesecore.properties
```
```sh
>:wq!
```
```sh
>: # vi ejbca.properties
```
```sh
>: #ejbca.profuctionmode=true
```
```sh
>: #ejbca.productionmode=false
```
```sh
>:wq!
```
```sh
>: # vi install.properties
```
```sh
>: wq!
```
```sh
>: # vi web.properties
```
```sh
>: # cd /opt
```
```sh
>: # sudo chown -R wildfly: ejbca_ce_7_4_0
```
```sh
>: # ls
```
```sh
>: # cd ejbca_ce_7_4_0/
```
```sh
>: ejbca_ce_7_4_0]# sudo -u wildfly ant -q clean deployer
```
```sh
>: # sudo -u wildfly ant -q runistall
```
```sh
>: # cd /opt/wildfly/bin
```
```sh
>: # . /jboss-cli.sh -c
```
```sh
 >:  /subsystem=remotin/http-connector=http-remoting-connector:remove
 total time : 2 seconds 
```
```sh
 >: # cd /opt/wildfly/bin
```
```sh
>: # ./jboss-cli.sh -c
```
```sh
 >: /subsystem=remotin/http-connector=http-remoting-connector:add(connector-ref= remoting",security - realm="applicationRealm"
 ```
```sh
 >:/socket-binding-group=standard-sockets/socket-binding=remoting:add (port="444")
 ```
```sh
 /subsystem=undertow/server=defalt-server/http-listener=remoting:add(socket-binding=remoting)
 ```
```sh
 >:reload
 ```
```sh
 >: subsystem=logging?kogger=onrg.ejbca:add
 ```
```sh
 >: subsystem=logging?kogger=onrg.ejbca:add
 ```
```sh
 >: subsystem=logging?kogger=onrg.ejbca:add
 ```
```sh
 >: subsytem=logging/logger=org.cesecore:add
 ```
```sh
 >: subsytem=logging/logger=org.cesecore:write-attribute(name=level, value=DEBUG)
 ```
```sh
 >: reload
 ```
```sh
quit
```
```sh
>:ls
```
```sh
>: cd /opt
```
```sh
>: ejbca_ce_7_4_0/
```
```sh
[root@localhost ejbca_ce_7_4_0]#
```
```sh
>: sudo -u wildfly ant -q runinstall3
```
```sh
>: initializing CA with 'EJBCA-management-CA',o=EJBCA POC,C=US' 'soft' '<ca.token
password hidden>' '4096' 'RSA' '10950' 'null' ' SHA256WIThRSA'   -superadmincn 'SuperAdmin...
```
```sh
>: batch tomcat
```
```sh
>: batch superadmincn
```
```sh
>: getting root certificate in DER format...
```
```sh
>: ca getcacert  "EJBCA-management-CA" /tmp/rootca.der -der
```
```sh
[root@localhost ejbca_ce_7_4_0]# sudo -u wildfly ant deploy-keystore
```
```sh
192.168.50.147.8080/ejbca/
```
```sh
>: # cd /opt/wildfly/bin
```
```sh
 >: # ./jboss-cli.sh -c
 ```
 ```sh
 >: /subsystem=undertow/server=default-server/http-listener=default:remove
 ```
 ```sh
 >: /socket-binding-group=standard-sockets-binding=http:remove
 ```
 ```sh
 >: reload
 ```
 ```sh
 >: /interface=http:add(inet-address="0.0.0.0")
 ```
 ```sh
 >: /interface=http:add(inet-address="0.0.0.0")
 ```
 ```sh
 >: /interface=http:add(inet-address="0.0.0.0")
 ```
```sh
 >: /interface=http:add(inet-address="0.0.0.0")
 ```
```sh
>: /socket-binding-group=standard-sockets/socket-binding=http:add(port="8080",interface
="http")
```
```sh
>: /subsystem=undertow/server=default-server/http:add(socket-binding=http
```
 ```sh
>: /subsystem=undertow/server=default-server/http-listener=http:write-attribute (name=re
direct-socket,value"httpspriv")
```
```sh
>:reload
```
```sh
>: /core-service=management/security-realm=SSLRealm:add()
```
```sh
>: /core-service=management/security-realm=SSLRealm/server-indenty=ssl:add(keystore-pa
th="S {jboss.server.config.dir}/keystore/keystore.jks",keystore-password=serverpwd", alias="localhost")
```
```sh
>: /core-service=management/security-realm=SSLRealm/server-indenty=ssl:add(keystore-pa
th="S {jboss.server.config.dir}/keystore/truststoretore.jks",keystore-password="changeint")
```
```sh
>: /socket-binding-group=standard-sockets/socket-binding=httpspriv:add(port="8443",interface="httpspriv")
```
```sh
>: /socket-binding-group=standard-sockets/socket-binding=httpspub:add(port="8442",interface="httpspub")
```
```sh
>: reload
```
```sh
>: /subsyatem=undertow/server=default-server/http-listener=httpspriv:add(socket-binding
=httpspriv, security-realm="SSLRealm", verify-client-REQUIRED)
```
```sh
>: /subsyatem=undertow/server=default-server/http-listener=httpspub:add(socket-binding=httpspub, security-realm"SSLRealm")
```
```sh
>: reload
```
```sh
>: /system-property=org.apache.tomcat.util.buf.UDecoder.ALLOW_ENCODED_SLASH:add(value=true)
```
```sh
>: /system-property=org.apache.catalina.connector.coyoteAdapter.ALLOW_BACKSLASH:add(value=true)
```
```sh
>: /system=property=org.apache.catalina.connector.URI_ENCODING:add(value="UTF-8")
```
```sh
>: /system-property=org.apache.catalina.connector.USE_BODY_ENCODING_FOR_QUERY_STRING:add(value=true)
```
```sh
>: /subsystem=webservices:write-attribute(name=wsdl-host, value=jbossws.undefined.host)
```
```sh
>: /subsytem=webservices:write-attribute(name=modify-wsdl-address, value=true)
```
 ```sh
>: :reload
```
```sh
>: quit
```
```sh
>: cd /opt/ejbca_ce_7_4_0/
```
```sh
>: ls
```
```sh
>:cd pq12
```
```sh
>: cd superadmincn.p12 /tmp
```
```sh
>: cd tmp
```
```sh
>: cd tmp
```
```sh
>: ls
```
```sh
>: chmod 755 superadmincn.p12
```





