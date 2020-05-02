![Magento 2 Docker](https://underser.github.io/static/magento.jpg)

# Docker for Magento 2 development

First of all, thank [rafaelstz](https://github.com/rafaelstz) this project is based on its [developments](https://github.com/clean-docker/Magento2)

### Apache 2.4 + (PHP 7.3 + OPCache + XDebug) + MariaDB + Redis + Elasticsearch 6.8

### Requirements

**MacOS:**

Install [Docker](https://docs.docker.com/docker-for-mac/install/), [Docker-compose](https://docs.docker.com/compose/install/#install-compose).

**You can view quick video tutorial which give you brief overview:**
![[Video tutorial how to install magento in your macos system](https://underser.github.io/static/apache-video-tutorial.png)](https://www.youtube.com/watch?v=OkTRY-AWQJw&t=1s)

**Linux:**

Install [Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/) and [Docker-compose](https://docs.docker.com/compose/install/#install-compose).

### How to use

Clone this repository:
```
git clone git@github.com:underser/magento2-docker.git <project_folder>
```
Go to <project_folder>:
```
./init
```
<sup>Script ask you about project name, and link to git repo</sup>

Put all your project files under ./src directory

Run:
```
docker-compose up -d
```
Copy all your files from host machine to container by running:
```
./bin/copytocontainer --all
```

After initialization you'll get 6 docker containers running:

| Container  | Ports(host/container)  | Description  |
|---|---|---|
| `<project_name>_apache`  | 80/80; 9000:9001; 443:443;  | Contains `Apache 2.4 + (PHP 7.3 + OPCache + N98 Magerun 2 + XDebug)` |
| `<project_name>_db`  | 3300/3306  | Contains `MariaDB` |
| `<project_name>_elasticsearch`  | 9200/9200  | Contains `Elasticsearch 6.8` |
| `<project_name>_mailhog`  | 1025/1025 ; 8025/8025  | Allow you reach emails from your app |
| `<project_name>_redis-session`  | n/6379  | Allow you save your sessions in Redis |
| `<project_name>_redis`  | n/6379  | Redis cache |

If you want execute ./bin/magento, simply do:
```
./magento <command>
```

During development you can fetch problem with permissions,
for example, when php process write file to your working directory,
and on host machine you can't change that file, to resolve this exec:
```
./permission
```
<sub>this will make sure that your host user id equals user id in container</sub>

Note: If you use OS X - to make XDebug working
exec this command in terminal
```
ifconfig lo0 alias 10.254.254.254
```

### License

MIT © 2020 [Roman Sliusar](https://github.com/underser/)
