https://github.com/zereyak13/DevOps/blob/master/sonarqube/Sonarqube_with_database.md

sudo su -
apt-get update  -y
apt-get install openjdk-11-jdk -y 

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'  
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get -y install postgresql

sudo passwd postgres
su - postgres

createuser sonar
psql
ALTER USER sonar WITH ENCRYPTED PASSWORD 'admin';
CREATE DATABASE sonarqube OWNER sonar;
GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;

\q

systemctl restart postgresql 
systemctl status postgresql

apt install net-tools

nano /etc/sysctl.conf
vm.max_map_count=524288
fs.file-max=131072
ulimit -n 131072
ulimit -u 8192

nano /etc/security/limits.conf
sonarqube   -   nofile   131072
sonarqube   -   nproc    8192

cd /opt
https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.9.56886.zip
unzip sonarqube-8.9.2.46101.zip


open it

