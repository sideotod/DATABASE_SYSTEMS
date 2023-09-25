![header](https://capsule-render.vercel.app/api?type=waving&color=auto&height=100&section=header&text=Week%203&fontSize=60&fontColor=black)

# PostgreSQL in Ubuntu
### 1. Installing PostgreSQL
> Updating apt(Advanced Packaging Tool) for installing and using postgreSQL
```bash
user@username $ sudo apt-get update
```
> Upgrade PostgreSQL version
<br>-   Update the list of apt(Advanced Packaging Tool)
```
user@username $ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release-cs)-pgdgmain" > /etc/apt/sources.list.d/pgdg.list'
```
```bash
user@username $ wget --quiet -O -https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudoapt-key add --

OK
```
```bash
user@username $ sudo apt update

... http://apt.postgresql.org/pub/repos/apt focal-pgdg... 
```
> Install PostgreSQL
```bash
user@username $ sudo apt-get postgresql-14 postgre-client-14
```
### 2. Excute PostgreSQL
> Login with Postgres account
```bash
user@username $ sudo -i -u postgres
```
> Excute psql terminal
```
postgres@username ~$ psql

psql(14.9 (Ubuntu 14.9-1.pgdg20.04+1))
Type “help” for help.

postgres=#
```
> Exit psql
```
# Command 1: \q
postgres=# \q
user@username $

# Command 2: quit
postgres=# quit
user@username $
```
> Make new account for user step 1 <br>- Login with postgres account
```bash
user@username $ sudo -i -u postgres
postgres@username ~$
```
> Make new account for user step 2<br> - Create account user for "me"
```bash
postgres@username ~$ createuser --interactive

Enter name of role to add: USER # "USER" should be same with user in "user"@username
shall the new role be a superuser? (y/n) y
```
> Make new account for user step 3<br>- Create database for "me"
```bash
postgres@username ~$ createdb USER
```
> Access PostgreSQL DBMS with USER account<br>- Logout
```
postgres@username ~$ exit
user@username $
```
#### **Note: Enter 'psql' directly, not in 'postgres@username ~$'**
```
user@username $ psql
user=# \conninfo

You are connected to database “USER” as user “USER” via socket in “/var/run/postgresql” at port “5432”.
```

### NOTE
#### If you have an ERROR, Please refer to the reference
> Error case 1.
```
user@username $ sudo -i -u postgres
postgres@username ~$ psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory 
        Is the server running locally and accepting connections on that socket?
```
This error message means that the postgres server is not connected.<br>
Therefore, the workaround is as follows:
```bash
# First, check that the postgres server is connected.
postgres@username ~$ ps -ef | grep postgres
# If there are no postgres server, we have to start postgreSQL database server.
postgres@username ~$ exit
logout
user@username $ sudo service postgresql start
* Starting PostgreSQL 14 database server                               [OK] 
```
> Error case 2.
```
None
```
### 3. Installing JDK
> Install JDK<br>- Install JDK for Ubuntu server
```bash
user@username $ sudo apt install openjdk-8-jdk-headless
```
> Download jdbc jar file
```
user@username $ wget https://jdbc.postgresql.org/download/postgresql-42.6.0.jar
user@username $ sudo mv postgresql-42.6.0.jar /usr/lib/jvm/java-8-openjdk-amd64/lib/
```
---
### Connection PostgreSQL with JDBC
1. Create connection with PostgreSQL (PostgresWithJDBCConnection.java)

2. Insert a record to PostgreSQL with JDBC (PostgresWithJDBCInsert.java)

3. Select a record to PostgreSQL with JDBC (PostgresWithJDBCSelect.java)

4. Update a record to PostgreSQL with JDBC (PostgresWithJDBCUpdate.java)

5. Delete a record to PostgreSQL with JDBC (PostgresWithJDBCDelete.java)

> Making java program
```
user@username $ vim programName.java
```
> Compile & Excute program
> >**javac** : Command for compiling Java source code.<br>Java compiler included in the Java Development Kit (JDK). This compiler transforms source code files into bytecode, which can be executed by the Java Virtual Machine (JVM).  'javac' command to compile a Java source file (.java), it generates a compiled bytecode file (.class)<br><br>**java** : Command for running Java applications.<br><br>**cp** : Option for specifying the classpath. In this case, it appears to include the path to the PostgreSQL JDBC driver JAR file.<br><br>**':/usr/lib/jvm/java-1.8.0-openjdk-amd64/lib/postgresql-42.6.0.jar'** : This part specifies the classpath. The classpath tells the JVM where to find the class files when the Java program is executed. In this case, it includes the path to the PostgreSQL JDBC driver JAR file.
<br><br>**programName.java** : The name of the Java source file to be compiled.
<br><br> **programName** : The name of the main class of the Java program to be executed.
```
user@username $ javac -cp ':/usr/lib/jvm/java-1.8.0-openjdk-amd64/lib/postgresql-42.6.0.jar' programName.java
user@username $ java -cp ':/usr/lib/jvm/java-1.8.0-openjdk-amd64/lib/postgresql-42.6.0.jar' programName
```
![Footer](https://capsule-render.vercel.app/api?type=waving&color=auto&height=100&section=footer)