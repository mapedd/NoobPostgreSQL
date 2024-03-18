# NoobPostgreSQL
Solutions to silly PosgreSQL problems

#1. Launching PosgreSQL servers
From what I can see, there are 3 popular ways of launching Postgres servers:
1. homebrew service [nice guide here](https://www.atlassian.com/data/admin/how-to-start-postgresql-server-on-mac-os-x)
   ```brew services start postgresql```
3. mac app [https://postgresapp.com/](Link)
4. standalone binary
5. docker container
   
#2. Managing PosteSQL databases
Seems there are few most important bits to configure when it comes to using Postgres DB, those are:
   1. DATABASE_HOST - this is essentially the network address of the database, so commonly you can see few cases:
      1. `localhost` - when you run simply postgres locally
      2. `db` - I saw that when running Postgres with docker. Docker contains have their own private networks so servies can refer to each other via nice DNS-like names
      3. `123.123.123.123` - some IP address when using a db server on different machine
   3. DATABASE_NAME - single postgres server can have multiple databases, each need to have a unique name.
      1. To create a database: `CREATE DATABASE new_db;` (remember semicolon)
      2. To delete database `DROP DATABASE new_db;` (remember semicolon)
      3. To show list of databases on given server: `postgres=# \l`
      4. Example output:
```
List of databases
      Name      |  Owner   | Encoding | Locale Provider |   Collate   |    Ctype    | ICU Locale | ICU Rules |   Access privileges   
----------------+----------+----------+-----------------+-------------+-------------+------------+-----------+-----------------------
 mapedd         | mapedd   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
 postgres       | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
 template0      | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
                |          |          |                 |             |             |            |           | postgres=CTc/postgres
 template1      | postgres | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
                |          |          |                 |             |             |            |           | postgres=CTc/postgres
 vapor_database | mapedd   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
 wheely         | mapedd   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
(6 rows)         
```
   5. DATABASE_USERNAME
   6. DATABASE_PASSWORD

      
#3. role "vapor_username" does not exist
```
[ WARNING ] PSQLError(code: server, serverInfo: [sqlState: 28000, file: miscinit.c, line: 756, message: role "vapor_username" does not exist, routine: InitializeSessionUserId, localizedSeverity: FATAL, severity: FATAL])
Swift/ErrorType.swift:200: Fatal error: Error raised at top level: PSQLError(code: server, serverInfo: [sqlState: 28000, file: miscinit.c, line: 756, message: role "vapor_username" does not exist, routine: InitializeSessionUserId, localizedSeverity: FATAL, severity: FATAL])
```

This problem might be caused by the fact that default Vapor DockerCompose file specifies `vapor_username` and `vapor_password` as credentials, where's :
1. default usename for most Unix distributions postgres
2. for homebrew, your mac user will be added as postgres user, probably it's beacue of `peer` authentication method

To solve the problem you can change values in docker compose files, or create the postgres user
1. [change defult user password](https://www.atlassian.com/data/admin/how-to-set-the-default-user-password-in-postgresql)
2. [add super user](https://www.atlassian.com/data/admin/how-to-change-a-user-to-superuser-in-postgresql)
3. [advanced user creation](https://www.atlassian.com/data/admin/create-a-user-with-psql)

# Tidbits

## Show postgres config file:
```
mapedd=# SHOW config_file;
                                config_file                                
---------------------------------------------------------------------------
 /Users/mapedd
```

# Interesting links
1. [Atlasian readme's](https://www.atlassian.com/data/admin/how-to-list-databases-and-tables-in-postgresql-using-psql#:~:text=Listing%20databases,command%20or%20its%20shortcut%20%5Cl%20.)
