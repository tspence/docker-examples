# Docker example scripts
This repository contains examples of Docker setup scripts I have developed that may be of use to others.

## SQL Server with full-text search
[SQL Server with full-text search](sqlserver-fulltext/Dockerfile) - A dockerfile build script that generates SQL Server and installs full-text search.  To use this dockerfile, you must specify the following environment variables:
* `SA_PASSWORD` - This must be a password that satisfies SQL Server's default password complexity requirements - it must include uppercase and lowercase letters, numbers, symbols, and must be at least 8 characters in length.
* `ACCEPT_EULA` - This must be set to the letter `Y` to allow SQL Server to start.

Example docker compose script:

```
version: "3.2"
services:

  sqlserver:
    container_name: sqlserver
    build:
      dockerfile: sqlserver-fulltext.Dockerfile
    ports:
      - "1433:1433"
    environment:
      SA_PASSWORD: "Some4Complex#Password"
      ACCEPT_EULA: "Y"
```
