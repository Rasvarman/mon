# mon
sudo -i
apt update
apt install postgresql
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
dpkg -i zabbix-release_6.4-1+debian11_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'13579\'';"'
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sed -i 's/# DBPassword=/DBPassword=13579/g' /etc/zabbix/zabbix_server.conf
systemctl restart zabbix-server apache2
systemctl enable zabbix-server apache2

sudo -i
apt update
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
dpkg -i zabbix-release_6.4-1+debian11_all.deb
apt update
apt install zabbix-agent
sed -i 's/Server=127.0.0.1/Server=10.0.2.15/g' /etc/zabbix/zabbix_agentd.conf
# На машине с Zabbix Server добавил 'Server=127.0.0.1,10.0.2.15' в файл /etc/zabbix/zabbix_agentd.conf
systemctl restart zabbix-agent
systemctl enable zabbix-agent


![Screenshot_166](https://github.com/user-attachments/assets/bc98bf76-f562-4216-85c3-64762f4d4369)
![Screenshot_165](https://github.com/user-attachments/assets/6b122294-b3e4-4bb7-b84c-68c6e7e81615)
![Screenshot_174](https://github.com/user-attachments/assets/77c67c6c-b356-43cd-a2b6-c153ba9b4ad2)
![Screenshot_173](https://github.com/user-attachments/assets/cf970dae-95fc-41ff-8583-c60185d286a2)
![Screenshot_172](https://github.com/user-attachments/assets/69274b80-6f90-4b84-89fb-d5d3799efaba)
![Screenshot_171](https://github.com/user-attachments/assets/231c3bf1-b6ae-4a98-abf8-96aafab56758)
![Screenshot_168](https://github.com/user-attachments/assets/94454d03-088d-4981-9103-baddf930e652)
