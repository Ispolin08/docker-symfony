# Docker containers for symfony application

## Intro
The idea is you can use this git repository for building php:7.1-fpm + nginx docker containers for run symfony applications fast 
and easy.  The containers name will be <CONTAINER_NAME_PREFIX>_php and <CONTAINER_NAME_PREFIX>_nginx. If you would like to run more than one project on same host just clone this repo for different folders. 

There is no mysql / redis / reverse proxy. I am using another containers with mysql, nginx, redis for sharing between 
all projects on one host. You will find containers for this services soon here. 


## Install 

- Clone this repo and run next commands:

```
cp ./.env.dist ./.env
cp ./nginx/symfony.conf.dist ./nginx/symfony.conf
chmod 755 rebuild-all
```

- Change parameters in this files as you need. 

If You are planning to use http auth you have to uncomment line in docker-compose.yml and
create .htpasswd file in ./nginx folder. This file will be mounted to container. Also you have
to uncomment lines in ./nginx/symfony.conf


- Run for rebuilding all containers
```
./rebuild-all
```

- Configure hosts file like 

```
127.0.0.1 dev1
```

- Run composer from inside docker container 

```
docker-compose exec -it php composer install

```

- Update database and do composer update if you want. Do it from php container.


## Check

Run 
```
docker -ps
```

Now you can see 2 new containers. 

If you run http://dev1:3000/app_dev.php you will get to your symfony application.


## Reverse proxy

