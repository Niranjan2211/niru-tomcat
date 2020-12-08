# Niru-tomcat

```
Tomcat in Docker Container

docker pull tutum/tomcat
docker run -d -p 8080:8080 -e TOMCAT_PASS="mypass" tutum/tomcat









```
How to Install tomcat.
prerequisite java need to be installed.
```

sudo yum install tomcat -y
sudo vi /usr/share/tomcat/conf/tomcat.conf  # add below parametesrs
JAVA_OPTS="-Djava.security.egd=file:/dev/./urandom -Djava.awt.headless=true -Xmx512m -XX:MaxPermSize=256m -XX:+UseConcMarkSweepGC"

Install Tomcat Admin packages:
    sudo yum install tomcat-webapps tomcat-admin-webapps
    sudo yum install tomcat-docs-webapp tomcat-javadoc

vi /usr/share/tomcat/conf/tomcat-users.xml
<tomcat-users>
...
</tomcat-users>

start and enable tomcat
    systemctl restart tomcat
    systemc enable tomcat

Validate: tomcat
http://server_IP_address:8080

cURL - Tomcat: 
```
[root@swarm01 my_work_space]# curl -s --user admin:admin http://192.168.9.86:8080/manager/text/list
OK - Listed applications for virtual host localhost
/:running:0:ROOT
/examples:running:0:examples
/sample:running:0:sample
/host-manager:running:0:host-manager
/manager:running:1:manager
/docs:running:0:docs
```


Stop microservice /docs
```
[root@swarm01 my_work_space]#  curl --user admin:admin http://192.168.9.86:8080/manager/text/stop?path=/docs
OK - Stopped application at context path /docs
```

Start Microservice /docs
```
[root@swarm01 my_work_space]#  curl --user admin:admin http://192.168.9.86:8080/manager/text/start?path=/docs
OK - Started application at context path /docs
[root@swarm01 my_work_space]#
```

##############################################################
See working files:--
```
[root@swarm01 my_work_space]# cat /usr/share/tomcat/conf/tomcat.conf
# System-wide configuration file for tomcat services
# This will be loaded by systemd as an environment file,
# so please keep the syntax. For shell expansion support
# place your custom files as /etc/tomcat/conf.d/*.conf
#
# There are 2 "classes" of startup behavior in this package.
# The old one, the default service named tomcat.service.
# The new named instances are called tomcat@instance.service.
#
# Use this file to change default values for all services.
# Change the service specific ones to affect only one service.
# For tomcat.service it's /etc/sysconfig/tomcat, for
# tomcat@instance it's /etc/sysconfig/tomcat@instance.

# This variable is used to figure out if config is loaded or not.
TOMCAT_CFG_LOADED="1"

# In new-style instances, if CATALINA_BASE isn't specified, it will
# be constructed by joining TOMCATS_BASE and NAME.
TOMCATS_BASE="/var/lib/tomcats/"

# Where your java installation lives
JAVA_HOME="/usr/lib/jvm/jre"
JAVA_OPTS="-Djava.security.egd=file:/dev/./urandom -Djava.awt.headless=true -Xmx512m -XX:MaxPermSize=256m -XX:+UseConcMarkSweepGC"

# Where your tomcat installation lives
CATALINA_HOME="/usr/share/tomcat"

# System-wide tmp
CATALINA_TMPDIR="/var/cache/tomcat/temp"

# You can pass some parameters to java here if you wish to
#JAVA_OPTS="-Xminf0.1 -Xmaxf0.3"

# Use JAVA_OPTS to set java.library.path for libtcnative.so
#JAVA_OPTS="-Djava.library.path=/usr/lib"

# Set default javax.sql.DataSource factory to apache commons one. See rhbz#1629162
JAVA_OPTS="-Djavax.sql.DataSource.Factory=org.apache.commons.dbcp.BasicDataSourceFactory"

# You can change your tomcat locale here
#LANG="en_US"

# Run tomcat under the Java Security Manager
SECURITY_MANAGER="false"

# SHUTDOWN_WAIT has been deprecated. To change the shutdown wait time, set
# TimeoutStopSec in tomcat.service.

# If you wish to further customize your tomcat environment,
# put your own definitions here
# (i.e. LD_LIBRARY_PATH for some jdbc drivers)
###################END OF FILE#################
```
```
[root@swarm01 my_work_space]# cat /usr/share/tomcat/conf/tomcat-users.xml
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <role rolename="admin-gui"/>
  <role rolename="admin-script"/>
  <user username="admin" password="admin" roles="manager-gui,manager-script,manager-jmx,manager-status,admin-gui,admin-script"/>
</tomcat-users>
################################################
```
##########################################################
Installtion of Tomcat 8
sudo yum install java-1.7.0-openjdk-devel
groupadd tomcat
sudo useradd -M -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
yum install wget
wget https://downloads.apache.org/tomcat/tomcat-8/v8.5.60/bin/apache-tomcat-8.5.60.tar.gz



