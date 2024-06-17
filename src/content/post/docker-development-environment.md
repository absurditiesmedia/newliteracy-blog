---
publishDate: "06 May 2024"
title: How to Use Docker for Development Environments
description: here's where I got stuck when trying to use docker. 
tags: ["docker", "development",  "devops", "system administration"]
coverImage:
    src: "../../assets/docker_logo.png"
    alt: "docker logo"
---

When developing an application running in Docker, you can edit the files on your local machine and have those changes immediately reflected in the running container. This is typically done using Docker volumes to mount your local project directory into the container. Here's how you can set this up:

### 1. Using Volumes in Docker Compose

In your docker-compose.yml file, use the volumes key to mount your local project directory to a directory inside the container. This allows you to edit files on your local machine, and the changes will be seen by the container in real-time.

Here's an example for a Node.js application:

`docker-compose.yml`
```
version: '3'
services:
  web:
    build: .
    ports:
      - "8080:8080"
    volumes:
      - .:/app
    depends_on:
      - db
  db:
    image: postgres:13
    environment:
      POSTGRES_USER: example
      POSTGRES_PASSWORD: example
      POSTGRES_DB: example
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```
In this configuration, the volumes section for the web service mounts the current directory (.) to the /app directory inside the container.

### 2. Ensure Your Application Watches for Changes

To take full advantage of real-time updates, your application should be configured to watch for file changes and automatically reload. Many development frameworks and languages have tools or libraries to facilitate this:

**Node.js:** Use nodemon to automatically restart the server when file changes are detected.

Install nodemon:

`npm install -g nodemon`

Update your Dockerfile to use nodemon:

`dockerfile:`

```
FROM node:14

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD ["nodemon", "app.js"]
```    

**Python/Flask:** Set the FLASK_ENV environment variable to development to enable the auto-reload feature.

Ensure your `docker-compose.yml` includes this:

```
yaml

    environment:
        FLASK_ENV: development
        FLASK_APP: app.py
```

### 3. Start Your Containers

With your Docker Compose file configured to use volumes, start your containers:

in your terminal run:
```
sh
docker-compose up
```


Now, any changes you make to the files in your local project directory will be reflected inside the container immediately.
Example for a Python Flask App

Here's a complete example for a Flask application, assuming you have a requirements.txt for your dependencies and app.py as your application entry point.


`Dockerfile`:
```
FROM python:3.9

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]
```


`docker-compose.yml`:
```
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    environment:
      FLASK_ENV: development
      FLASK_APP: app.py
    depends_on:
      - db
  db:
    image: blogpostgres:13
    environment:
      POSTGRES_USER: example
      POSTGRES_PASSWORD: example
      POSTGRES_DB: example
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

With this setup, you can work on your Flask application in your local editor, and the changes will be applied immediately in the running container.
Summary

- Mount your local directory into the container using volumes: This allows real-time file changes.
- Use tools like nodemon (for Node.js) or Flask's development mode: These tools detect file changes and reload the application automatically.
- Start your Docker containers with docker-compose up: This will ensure your development environment is set up correctly and changes are reflected immediately.

This approach provides a seamless development experience with Docker, allowing you to edit code on your local machine while the application runs inside containers.

[last:why use docker](/posts/why-use-docker)