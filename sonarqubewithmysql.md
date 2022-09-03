vpc kuruldu

scp -i ./awsEC2.pem ./awsEC2.pem ubuntu@18.232.137.31://home/ubuntu/

    Ec2 

sudo apt-get update
sudo apt-get install openjdk-8-jdk -y

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.3.1.34397.zip 

sudo apt install unzip

mv sonarqube-8.3.1.34397.zip /opt

cd  /opt

unzip sonarqube-8.3.1.34397.zip 

cd sonar
sudo useradd sonaradmin
sudo passwd sonaradmin/sonaradmin

chown -R sonaradmin:sonaradmin sonarqube-8.3.1.34397

        RDS
DB instance identifier
sonarqubedb

Master username
sonaradmin-sonaradmin

Database options
sonarqubedb

RDS ---> subnet group 
sudo apt install mysql-client-core-8.0 -y
sudo apt install mariadb-client-core-10.6 -y

sudo apt install mysql-server-core-8.0 -y
sudo apt install mariadb-server-10.6 -y

sudo systemctl start mariadb
sudo systemctl enable mariadb

mysql -h endpoint -u sonaradmin -p

USE mysql;
CREATE DATABASE sonardb;

create user sonar@localhost identified by 'sonar1234';
create user sonar@'%' identified by 'sonar1234';

grant all on sonardb.* to sonar@localhost;
grant all on sonardb.* to sonar@'%';

FLUSH PRIVILEGES;
SELECT Host, User, Password FROM user; local ve remot user
quit

cd /opt/sonarqube-8.3.1.34397/
cd conf/
ls
nano sonar.properties

#----- MySQL 5.x
# Only InnoDB storage engine is supported (not myISAM).
# Only the bundled driver is supported. It can not be changed.
sonar.jdbc.url=jdbc:mysql://endpoint:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance

webserver kismi /sonar ve port acilacak

cd bin
cd linux
./sonar.sh start
./sonar.sh status

