# Dockerized Liquibase

[![Docker Pulls](https://img.shields.io/docker/pulls/ferrarimarco/liquibase.svg)](https://hub.docker.com/r/ferrarimarco/liquibase/)
[![Docker Automated build](https://img.shields.io/docker/automated/ferrarimarco/liquibase.svg)](https://hub.docker.com/r/ferrarimarco/liquibase/)

[![Build Status Master Branch](https://travis-ci.org/ferrarimarco/docker-liquibase.svg?branch=master)](https://travis-ci.org/ferrarimarco/docker-liquibase)

This is a [Liquibase](http://www.liquibase.org) instance running in a Docker container.

Part of the [Open Development Environment Project](https://github.com/ferrarimarco/open-development-environment).

The following drivers have been included:

- H2 JDBC 1.4.195
- Oracle JDBC 8 12.2.0.1
- Mysql 5.1.47
- postgresql 9


## Supported tags and respective Dockerfile links
- `3.6.1`, `latest` [(Dockerfile)](https://github.com/ferrarimarco/docker-liquibase/blob/3.6.1/Dockerfile)
- `master-latest` [(Dockerfile)](https://github.com/ferrarimarco/docker-liquibase/blob/master/Dockerfile)


## How to run

### Query the status of the database

Get the list of changesets to apply considering a database and a changelog to apply

```
docker run --rm -it -v /path/to/changelog/dir/on/the/host/:/liquibase/changelog/ \
  ferrarimarco/liquibase \
  --driver=oracle.jdbc.OracleDriver \
  --changeLogFile=/liquibase/changelog/changelog-name.yaml \
  --url=jdbc:oracle:thin:@DB_HOST:DB_PORT/DB_NAME \
  --username=DB_USER \
  --password=DB_PW \
  status
```

### Generate a Liquibase diff report

```
docker run --rm -it ferrarimarco/liquibase \
  --driver=oracle.jdbc.OracleDriver \
  --referenceUrl=jdbc:oracle:thin:@REF_DB_HOST:REF_DB_PORT/REF_DB_NAME \
  --referenceUsername=REF_DB_USER \
  --referencePassword=REF_DB_PW \
  --url=jdbc:oracle:thin:@DB_HOST:DB_PORT/DB_NAME \
  --username=DB_USER \
  --password=DB_PW \
  diff
```

### Generate a Liquibase diff changelog report

```
docker run --rm -it -v /path/to/changelog/dir/on/the/host/:/liquibase/changelog/ \
  ferrarimarco/liquibase \
  --driver=oracle.jdbc.OracleDriver \
  --changeLogFile=/liquibase/changelog/changelog-name.yaml \
  --referenceUrl=jdbc:oracle:thin:@REF_DB_HOST:REF_DB_PORT/REF_DB_NAME \
  --referenceUsername=REF_DB_USER \
  --referencePassword=REF_DB_PW \
  --url=jdbc:oracle:thin:@DB_HOST:DB_PORT/DB_NAME \
  --username=DB_USER \
  --password=DB_PW \
  diffChangeLog
```

Note that if you change the `--changeLogFile` extension to .xml, Liquibase will generate a changelog in XML format.

### Apply a changelog to the database

```
docker run --rm -it -v /path/to/changelog/dir/on/the/host/:/liquibase/changelog/ \
  ferrarimarco/liquibase \
  --driver=oracle.jdbc.OracleDriver \
  --changeLogFile=/liquibase/changelog/changelog-name.yaml \
  --url=jdbc:oracle:thin:@DB_HOST:DB_PORT/DB_NAME \
  --username=DB_USER \
  --password=DB_PW \
  update
```

### Generate a SQL script to update a database (considering its current status) from a changelog

```
docker run --rm -it -v /path/to/changelog/dir/on/the/host/:/liquibase/changelog/ \
  ferrarimarco/liquibase \
  --driver=oracle.jdbc.OracleDriver \
  --changeLogFile=/liquibase/changelog/changelog-name.yaml \
  --url=jdbc:oracle:thin:@DB_HOST:DB_PORT/DB_NAME \
  --username=DB_USER \
  --password=DB_PW \
  updateSQL
```
