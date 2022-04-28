# Useful Docker Composes

A repository to host some docker-compose yaml configuration tha may be useful for developing

The files will be organized in folders with the initial of the referred system.

The INDEX file can take you directly to desired system.

## Contribution

Feel free to contribute to this repo! There are few rules to follow:

1. Put the file in a folder of the initial of the system. If it not exists, feel free to create it yourself. Eg.: **rabbit-mq.yaml** at the **R** folder.

2. Edit the INDEX.md putting a link direct to the github provided raw version of the file in the letter of you system, if possible at alphabetic order.

3. Explain clearly points in the file that must be replaced by environment variables or personal data such as volume paths or passwords. You can leave comments in the file if you want.

## Branch names

Create branches for pull requests following this convention.

`new-some-new-system-yaml` for new docker-compose files.

`fix-some-fixed-system-yaml` for fixes or enhancements in a existent compose configuration.

## Problems?

Feel free to open issues about some problem in some configuration file. As well feel free to propose solutions and enhancements.

## Example

An example for a configuration for using PostgreSQL and PGAdmin

```yaml
version: '3'

services:
  postgres-compose:
    image: postgres
    environment:
      POSTGRES_PASSWORD: "some-password-you-want"
    ports:
      - "5432:5432"
    volumes:
      # A folder where you want to map as postgres persistent data volume
      - my-docker-volumes-folder:/var/lib/postgresql/data
    networks:
      - postgres-compose-network
      
  pgadmin-compose:
    image: dpage/pgadmin4:6.8
    environment:
      # The email you'll use to login to PGAdmin, must not be a true address
      PGADMIN_DEFAULT_EMAIL: "alantelles@alan.telles"
      # Password for this account
      PGADMIN_DEFAULT_PASSWORD: "mydevpassword"
    ports:
      - "16543:80"
    depends_on:
      - postgres-compose
    networks:
      - postgres-compose-network

networks: 
  postgres-compose-network:
    driver: bridge

```

