# Change Data Capture with Debezium
Debezium is among the Apache tools that are made using Java. As such, understanding java is critical. See linked for intro to Java needed to understand CDC with Debezium

# Event-Driven approach for CDC
An event-driven program (i.e. reacting to a change instead of exploring for a change) is executed when a program detects that an event has occured, such as a change to the database. An event could be if a new record is inserted or an existing record is updated. These events can be programmatically searched and captured. CDC packages are available to propogate changes to other applications. In fact, most data stores maintain a transaction log. 

# What Is Debezium?

It is understood that CDC is extremely useful when trying to synchronize multiple databases and systems. In [this](https://github.com/aarondaniels/Change_Data_Capture) repo, I demonstrate how CDC techniques are implemented for efficient maintenance of data. However, instead of manually propagating the necessary changes throughout your databases, you can take advantage of a platform that can help you with that: Debezium.

Debezium is an open-source distributed platform for CDC. Debezium can point at your databases, and your applications can start responding to all of the inserts, updates, and deletes that other applications commit to your databases.

To understand exactly what Debezium does, let’s consider an example. Suppose you have a database called customers that has a table called customers in it. One of the features of your application is to produce a daily report of the top 500 customers. This means that, ideally, you would like to generate a report of the customers table that includes record additions, modifications, and deletions.

As you can imagine, implementing these changes manually on a daily basis can quickly become expensive, and the process is extremely prone to errors.

Debezium comes handy at this stage because it pushes changes out to your application as they happen. In other words, it streamlines the process of monitoring your database and producing your desired report.

## How Does Debezium Interact with Different Types of Databases?

Debezium’s architecture is built around the concept of connectors, or a process that moves data from one database to another. These processes may allow for filtering data, transforming it into a desired structure, or updating it for the purposes of analysis in a similar way as it happens in CDC.

Debezium is a library of connectors that capture changes from a variety of database management systems making it easier for your applications to consume and respond to the events regardless of where the changes originated. Each connector is designed for a specific type of database by taking advantage of that specific database feature for CDC.

Currently, Debezium supports connectors for the following databases that you are already familiar with: MySQL, MongoDB, and Cassandra.

## The following steps will be taken to implement CDC by setting up a Debezium container for MySQL:
### Create a MySQL database server within a container, initialize it, and make the container part of a network (see [this](https://github.com/aarondaniels/change_data_capture_debezium/blob/main/Docker_info/networks.md) doc for instruction on container networks)
1. Create Docker File, which references the sql file that creates the database. In this case, see [this file](https://github.com/aarondaniels/change_data_capture_debezium/blob/main/Database/Dockerfile)
2. Create a docker netwowrk by entering the following in the CLI `docker network create myCDCNetwork`
2. Create Docker Image by entering the following in the command line
```
docker build -t mysqlmasterimg .
```
Confirm image was created by entering `docker images` in the command line and finding the new image. 
3. Create a Docker container
```
docker run --rm --name mysqlserver -p 33061:3306 --network myCDCNetwork -d mysqlmasterimg
```
Of mention, this command adds the container to the network of interest. In this case, 'mysqlable'



### Run Debezium in a container
1. Using the [DebeziumApp folder](https://github.com/aarondaniels/change_data_capture_debezium/tree/main/DebeziumApp), build a ***docker image*** by navigating to the DebeziumApp folder in command line an entering the following command, `docker build -t debeziumimg .`
2. From the command line, run the following command to create a ***Debezium container***
```
docker run -it --rm --name debeziumserver --network myCDCNetwork debeziumimg bash
```
Ensure the container is part of the same network as the MySQL server container
3. Within the Debezium server container, navigate to /tmp/src/main/java/mit/edu/tv/config/DebesiumConnectorConfig.java and ensure the config file has the appropriate database noted. In this case, employeedb. 
3. From the command prompt, run the following command to start the Spring Boot application that uses Debezium to monitor the MySQL database: 
```
mvn spring-boot:run
```

### Bring it all together

1. Connect via the workbench and add database data. Open MySQL workbench and connect to the customerdb file that is running inside the docker container created above. Run the INSERT query to insert a new row in the customer table: 
``` sql

INSERT INTO employeedb.employee VALUES (2, "Mary", "Doe", "4351234354", "mary@doe.com");
```
At this point, the Debezium console application should indicate that a new row was created in the customer table from Workbench.


