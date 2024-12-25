# Step by Step
1. start with docker-compose
```shell
docker-compose up -d
```

2. connect with terminal
```shell
# install clickhouse-cli first, use google to find how to install it

# default username and password is in .env file
clickhouse-cli -u default -B test

# do everything you want, such as create database, create table, insert data, etc.
```

3. open browser and visit `http://127.0.0.1:5521/`
