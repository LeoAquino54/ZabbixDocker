# ZabbixDocker
Instalação do Zabbix via Docker


docker pull mysql
<br>
docker pull zabbix/zabbix-server-mysql
<br>
docker pull zabbix/zabbix-web-nginx-mysql
<br>
docker pull zabbix/zabbix-java-gateway
<br>
docker pull zabbix/zabbix-agent
<br>

docker run --name mysql-server -t -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="user" -e MYSQL_PASSWORD="senha" -e MYSQL_ROOT_PASSWORD="YjA0OTYwZDBiN2EwNWFjMTRjZGU3Yjcy" -d mysql --character-set-server=utf8 --collation-server=utf8_bin --default-authentication-plugin=mysql_native_password
<br>
<br>
<br>

docker run --name zabbix-java-gateway -t --restart unless-stopped -d zabbix/zabbix-java-gateway
<br>
<br>

docker run --name zabbix-server-mysql -t -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="user" -e MYSQL_PASSWORD="senha" -e MYSQL_ROOT_PASSWORD="YjA0OTYwZDBiN2EwNWFjMTRjZGU3Yjcy" -e ZBX_JAVAGATEWAY="zabbix-java-gateway" --link mysql-server:mysql --link zabbix-java-gateway:zabbix-java-gateway -p 10051:10051 --restart unless-stopped -d zabbix/zabbix-server-mysql
<br>
<br>
<br>

docker run --name zabbix-web-nginx-mysql -t -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="user" -e MYSQL_PASSWORD="senha" -e MYSQL_ROOT_PASSWORD="YjA0OTYwZDBiN2EwNWFjMTRjZGU3Yjcy" --link mysql-server:mysql --link zabbix-server-mysql:zabbix-server -p 80:8080 --restart unless-stopped -d zabbix/zabbix-web-nginx-mysql
<br>
<br>
<br>

docker run --name zabbix-agent --link mysql-server:mysql --link zabbix-server-mysql:zabbix-server -e ZBX_HOSTNAME="Zabbix server" -e ZBX_SERVER_HOST="zabbix-server" -d zabbix/zabbix-agent

<br>
<br> 

Ou utilize o comando docker run --name zabbox-appliance -p 90:80 -p 10051:10051 -d zabbix/zabbix-appliance

