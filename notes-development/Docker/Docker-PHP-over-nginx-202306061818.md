---
title: Docker-PHP-over-nginx
date: 06/06/2023
tags: docker devops php nginx
---

# **Docker-PHP-over-nginx** 202306061818 
> **8eb32b**


## A docker container to run PHP[1]

To create a Docker container running PHP over Nginx, you can follow these steps:

1. Install Docker: Ensure that Docker is installed on your system. You can download and install Docker Desktop from the official Docker website (https://www.docker.com/products/docker-desktop).

2. Create a Dockerfile: In the directory where you want to create your Docker container, create a file named Dockerfile (without any file extension). Open the file in a text editor and add the following content:

```dockerfile
# Base image
FROM php:latest

# Install nginx
RUN apt-get update && apt-get install -y nginx

# Copy nginx configuration
COPY nginx.conf /etc/nginx/sites-available/default

# Set working directory
WORKDIR /var/www/html

# Copy PHP files
COPY . .

# Expose port 80
EXPOSE 80

# Start nginx and PHP
CMD service nginx start && php-fpm

```

3. Create Nginx Configuration: Create a file named nginx.conf in the same directory as the Dockerfile and add the following content:

```nginx
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}

```

4.   Place PHP files: Put your PHP files in the same directory as the Dockerfile.
    
5.  Build the Docker image: Open a terminal or command prompt, navigate to the directory containing the Dockerfile, and run the following command to build the Docker image:

`docker build -t my-php-nginx-app .`

6. Run the Docker container: Once the image is built, you can run the container using the following command:

`docker run -p 8080:80 my-php-nginx-app`

[1]: https://chat.openai.com/share/9c35d927-e9e7-4061-830a-cef90e5bc549