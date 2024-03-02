---
title: 'Tools: Nginx Proxy Manager'
abbrlink: 2b05a48d
date: 2024-03-02 10:00:00
tags:
  - Nginx
  - Docker
categories:
  - Tools
cover: https://p.wzsco.top/4a6fbfd50a5353df2a793ac23221c896.png/cover
---

*[Nginx Proxy Manager]: A pre-built docker image that enables you to easily forward to your websites running at home or otherwise, including free SSL, without having to know too much about Nginx or Letsencrypt.

## Introduction

This project comes as a pre-built docker image that enables you to easily forward to your websites running at home or
otherwise, including free SSL, without having to know too much about Nginx or Letsencrypt.

[Nginx Proxy Manager](https://github.com/jc21/nginx-proxy-manager)

## Features

* Beautiful and Secure Admin Interface based on Tabler
* Easily create forwarding domains, redirections, streams and 404 hosts without knowing anything about Nginx
* Free SSL using Let's Encrypt or provide your own custom SSL certificates
* Access Lists and basic HTTP Authentication for your hosts
* Advanced Nginx configuration available for super users
* User management, permissions and audit log

## Quick Setup

**Ubuntu 20.04**

1. Install Docker and Docker-Compose
   ```bash
   sudo apt-get update
   sudo apt-get install docker.io
   sudo apt-get install docker-compose
   ```
2. Create a new directory for the Nginx Proxy Manager
   ```bash
   mkdir ~/.nginx-proxy-manager
   cd ~/.nginx-proxy-manager
   ```
3. Create a docker-compose.yml file similar to this:
    ```yaml
    version: '3.8'
    services:
      app:
        image: 'jc21/nginx-proxy-manager:latest'
        restart: unless-stopped
        ports:
          - '80:80'
          - '81:81'
          - '443:443'
        volumes:
          - ./data:/data
          - ./letsencrypt:/etc/letsencrypt
    ```
   if you want to use a database for the Nginx Proxy Manager, you can add a MariaDB service to the docker-compose.yml
   file:
   ```yaml
   version: '3.8'
   services:
     app:
       image: 'jc21/nginx-proxy-manager:latest'
       restart: unless-stopped
       ports:
         - '80:80'
         - '81:81'
         - '443:443'
       volumes:
         - ./data:/data
         - ./letsencrypt:/etc/letsencrypt
       environment:
         DB_MYSQL_HOST: "db"
         DB_MYSQL_PORT: 3306
         DB_MYSQL_USER: "npm"
         DB_MYSQL_PASSWORD: "npm"
         DB_MYSQL_NAME: "npm"
     db:
       image: 'jc21/mariadb-aria:latest'
       restart: unless-stopped
       environment:
         MYSQL_ROOT_PASSWORD: 'npm'
         MYSQL_DATABASE: 'npm'
         MYSQL_USER: 'npm'
         MYSQL_PASSWORD: 'npm'
       volumes:
         - ./data/mysql:/var/lib/mysql
   ```
   **Mysql**
   ```yaml
   version: '3.8'
   services:
     app:
       image: 'jc21/nginx-proxy-manager:latest'
       restart: unless-stopped
       ports:
         - '80:80'
         - '81:81'
         - '443:443'
       volumes:
         - ./data:/data
         - ./letsencrypt:/etc/letsencrypt
       environment:
         DB_MYSQL_HOST: "db"
         DB_MYSQL_PORT: 3306
         DB_MYSQL_USER: "npm"
         DB_MYSQL_PASSWORD: "npm"
         DB_MYSQL_NAME: "npm"
     db:
       image: 'mysql:5.7'
       restart: unless-stopped
       environment:
         MYSQL_ROOT_PASSWORD: 'npm'
         MYSQL_DATABASE: 'npm'
         MYSQL_USER: 'npm'
         MYSQL_PASSWORD: 'npm'
       volumes:
         - ./data/mysql:/var/lib/mysql
   ```
4. Start the Nginx Proxy Manager
   ```bash
   docker-compose up -d
   # if using docker compose plugin
   docker compose up -d
   ```
5. Access the Nginx Proxy Manager at http://localhost:81(default) and log in with the default username and password:
    - `Email:    admin@example.com`
    - `Password: changeme`

## Reference

- [Nginx Proxy Manager](https://nginxproxymanager.com/)
- [Nginx Proxy Manager GitHub](https://github.com/jc21/nginx-proxy-manager)
- [Nginx](https://www.nginx.com/)
- [Docker](https://www.docker.com/)

## Screenshots

|                                      Screenshots                                      |                                      Screenshots                                       |
|:-------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------:|
|    ![Login View](https://p.wzsco.top/6f05522d0daa87e420d10e28b65a6ebe.png/blogimg)    |     ![Home View](https://p.wzsco.top/09f7e8ba13575825f987435c415ff834.png/blogimg)     |
| ![Proxy Hosts View](https://p.wzsco.top/0c686ec680575d12b1921a6a34ff06b9.png/blogimg) |  ![New Proxy View](https://p.wzsco.top/5538a9f745a8d513a4c6e70b39478aaa.png/blogimg)   |
|  ![Audit Log View](https://p.wzsco.top/11323c33e303badb222a25f9e0b316b7.png/blogimg)  | ![Default Site View](https://p.wzsco.top/2b831c14fbfbf7dd6d4a83190fbc7e9c.png/blogimg) |