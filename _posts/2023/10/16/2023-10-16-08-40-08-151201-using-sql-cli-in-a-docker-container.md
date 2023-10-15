---
layout: post
title: "Using SQL CLI in a Docker container"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

Docker containers provide a convenient way to run applications in a isolated and portable environment. In this blog post, we will explore how to use SQL CLI (Command Line Interface) in a Docker container to interact with a database.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up a Docker container](#setting-up-a-docker-container)
- [Accessing a database in the Docker container](#accessing-a-database-in-the-docker-container) 
- [Conclusion](#conclusion)
- [References](#references)

## Prerequisites<a name="prerequisites"></a>
Make sure Docker is installed on your machine. You can download and install Docker from the official website [here](https://www.docker.com/).

## Setting up a Docker container<a name="setting-up-a-docker-container"></a>
1. First, pull the SQL CLI Docker image by running the following command in your terminal or command prompt:

```bash
docker pull microsoft/mssql-cli
```

2. Once the image is pulled, you can create a new Docker container with the following command:

```bash
docker run -it --rm --name sql-cli-test microsoft/mssql-cli
```

- The `-it` flag allocates an interactive pseudo-tty for the container.
- The `--rm` flag automatically removes the container when it exits.
- The `--name` flag specifies a name for the container. You can choose any name you prefer.

## Accessing a database in the Docker container<a name="accessing-a-database-in-the-docker-container"></a>
Now that you have the SQL CLI Docker container up and running, you can connect to a database by running the following command inside the container:

```bash
mssql-cli -S <server_name> -U <username> -P <password> -d <database_name>
```

Replace `<server_name>`, `<username>`, `<password>`, and `<database_name>` with your database connection details.

Once connected, you can execute SQL queries and interact with the database through the SQL CLI.

## Conclusion<a name="conclusion"></a>
Using SQL CLI in a Docker container provides a portable and isolated environment for managing and querying databases. It allows you to quickly set up a database environment without worrying about installation and configuration.

With SQL CLI and Docker, you have a powerful toolset for working with databases in a convenient and reproducible manner.

## References<a name="references"></a>
- [Docker website](https://www.docker.com/)
- [Microsoft SQL CLI Docker image](https://hub.docker.com/r/microsoft/mssql-cli/)