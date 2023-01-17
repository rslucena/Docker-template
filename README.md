# Docker Template
_A simple structure used as a basis for creating new projects. The main idea is to have a quick project start and evolve as needed._
>Note: Under construction

### Tech

- [Docker](https://www.docker.com/): Is a platform designed to help developers build, share, and run modern applications. We handle the tedious setup, so you can focus on the code.

- [Nginx(stable-alpine)](https://www.nginx.com/): Nginx is a lightweight HTTP server, reverse proxy, IMAP/POP3 mail proxy, made by Igor Sysoev in 2005, under BSD-like 2-clause license.

- [PHP (8.2-FPM)](https://www.php.net/): A popular general-purpose scripting language that is especially suited to web development.

- [Redis (stack-server)](https://redis.io/): Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache, and message broker.

- [Mysql (latest)](https://www.mysql.com/): Is a database management system, which uses the SQL language as an interface.

>Note: The choices were born out of experience and common usage in most of the projects I've been involved with.

## Structure

| Folder               | Description                                                |
| ----------------- | ---------------------------------------------------------------- |
| .docker       | All configuration files separated by services |
| application       | All application files |

|   Folder    | Description |   Nginx/PHP   |
| ----------  | ------------ | ------------  |
|   application/App/multithread.php  | Swoole PHP Files (multithread) | 88:1215 |
| application/App/singlethread.php  | PHP Runtime Files (singlethread) | 85:9000 |

| Folder | Description | Nginx |
| ----------  | ------------ | ------------  |
| application/Public  | Static files or public files | 80:80 |
| application/Logs  | Separate log files per service | - |
| application/Vendor  | Third-party package files | - |

## Startup

> You first need to have [Docker](https://www.docker.com/get-started/) installed.

After installing and having Docker running, it is necessary to create the necessary files to use `docker-compose`

```sh
cp exemple.env .env
rm exemple.env
```
Fill in all the variables according to your needs

-- `ENV` used to further define dynamic properties between development and production.

-- `REDIS_SERVER` Name server

-- `MYSQL_SERVER` Name server

-- `MYSQL_MAX_CONNECTIONS` MySQL maximum connection limit.

-- `MYSQL_USER` database user name.

-- `MYSQL_PASSWORD` database password.

-- `MYSQL_DATABASE` database name.

-- `MYSQL_INITDB_SKIP_TZINFO` the entrypoint script automatically loads the timezone data needed for the CONVERT_TZ() function. If it is not needed, any non-empty value disables timezone loading.

-- `MYSQL_INNODB_LOG_FILE_SIZE` dictates the size in bytes of the commit log files stored by MySQL.

-- `MYSQL_INNODB_BUFFER_POOL_SIZE` the MySQL configuration parameter that specifies the amount of memory allocated to the InnoDB buffer pool by MySQL.

-- `MYSQL_ALLOW_EMPTY_PASSWORD` Set it to true to allow the container to be started with a blank password for the root user.

-- `MYSQL_ROOT_PASSWORD` Root password to access and manipulate MySQL settings.

-- `REDIS_PASS` Redis Authentication Password

## Creation of containers

In the root of the project, after having configured all the necessary environment variables, just run the command and wait for all the additional files to be created

```sh
 docker-compose up -d --build
```

If you want to follow the creation process to check possible errors, just run the command removing the `-d`

```sh
 docker-compose up --build
```


## Development

Some of the configurations still need to be tested or implemented. If you are interested in helping the process, feel free to suggest updates. The more people working for the next one, the better! :)

You will also notice that most PHP extensions are not installed, this is by design, the idea is that we have virtually no extensions installed by default. We take everything to the Env and from there manipulate the Dockerfile to install what is needed for each project.
