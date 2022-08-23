# Docker Networks

In order for database containers to propogate changes they need to be connected. Docker accomplishes this by putting the containers of interest in a docker network. 

## How to create a network? 
1. Run the following command from the PowerShell `docker network create myCDCNetwork`
2. In VS Code, create a file called, `customer.sql` and add the following code block: 
``` sql
CREATE DATABASE IF NOT EXISTS customerdb;

USE customerdb;

DROP TABLE IF EXISTS `customer`;

CREATE TABLE `customer` (
   `id` int not null,
   `fullname` varchar(255) default null,
   `email` varchar(255) default null,
   PRIMARY KEY (`id`)
);

INSERT INTO customerdb.customer VALUES (1, 'John Doe', 'jd@example.com');
```
As inferred, this script will create a database, then create  table within the database, and finally add a line of data to the table.

3. In the same folder, create a dockerfile with the following content:
``` 
FROM mysql:8.0

ENV MYSQL_DATABASE=customerdb \
    MYSQL_ROOT_PASSWORD=MyNewPass

ADD customer.sql /docker-entrypoint-initdb.d

EXPOSE 3306
```
4. Create a MySQL docker container and associate it to the myCDCNetwork with the following commandd: 
```
docker run --rm --name mysqlserver -p 3306:3306 --network myCDCNetwork -d mysqltest
```
Confirm this is working by inspecting the Docker dashboard for the mysqltest container

