# meinerstesrepo
cd ./Projektverzeichnis/myjoomla/
docker build -t bign0se/myjoomla:1.0
cd ./Projektverzeichnis/mydb/
docker build -t bign0se/mydb:1.0
docker push bign0se/myjoomla:1.0
docker push bign0se/mydb:1.0
docker network create mynetwork
docker run -d -v mydb_data:/var/www/html/ --net mynetwork -e MYSQL_ROOT_PASSWORD="Admin" --name mydb bign0se/mydb:1.0
docker run -d -p 8080:80 -v myjoomla_data:/var/www/html/ --net mynetwork -e JOOMLA_DB_HOST=mydb:3306 -e JOOMLA_DB_PASSWORD=Admin -e JOOMLA_DB_USER=root --name myjoomla bign0se/myjoomla:1.0
docker exec -it mydb /bin/bash
mysql -u root -p 
SHOW DATABASES;
exit
# erm What the sigma
