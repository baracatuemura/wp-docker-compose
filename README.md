# WPDC - WordPress Docker Compose

Easy setup local WordPress development enviroment with Docker and Docker Compose.

With this project you can quickly run the following:

- [WordPress and WP CLI](https://hub.docker.com/_/wordpress/)
- [phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
- [MySQL](https://hub.docker.com/_/mysql/)

## Requirements

Make sure you have the latest versions of **Docker** and **Docker Compose** installed on your machine.

**MacOS:**

Install [Docker](https://docs.docker.com/docker-for-mac/install/), [Docker-compose](https://docs.docker.com/compose/install/#install-compose) and [Docker-sync](https://github.com/EugenMayer/docker-sync/wiki/docker-sync-on-OSX).

**Windows:**

Install [Docker](https://docs.docker.com/docker-for-windows/install/), [Docker-compose](https://docs.docker.com/compose/install/#install-compose) and [Docker-sync](https://github.com/EugenMayer/docker-sync/wiki/docker-sync-on-Windows).

**Linux:**

Install [Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/) and [Docker-compose](https://docs.docker.com/compose/install/#install-compose).

Make sure to [add your user to the `docker` group](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user) when using Linux.


## How to use

Execute in your terminal, change the *WPFOLDER* to use the name of your project:

### Clone repository

```
git clone https://github.com/baracatuemura/wordpress-docker-compose.git WPFOLDER
```
### For new WordPress instalation 

```
cd WPFOLDER
cp env.example .env
./start
cp -R wp-app/wp-content/themes/ src/
cp -R wp-app/wp-content/plugins/ src/
```

In browser go to http://127.0.0.1

### For WordPress existing source

```
cd WPFOLDER
cp env.example .env
mkdir wp-data
```

* copy the database dump to `wp-data` folder
* copy `themes`, `plugins` and `uploads` folders to `src` folder

```
./start
```
#### Replace data base URLs 
```
docker-compose run --rm wpcli search-replace 'http://mysite.com' 'http://127.0.0.1'
```

In browser go to http://127.0.0.1

## Configuration

Copy the example environment into `.env`

```
cp env.example .env
```

Edit the `.env` file to change the default IP address, MySQL root password and WordPress database name.


## Usage

### Starting containers

You can start the containers with the `up` command in daemon mode (by adding `-d` as an argument) or by using the `start` command:

```
./start
```
or
```
docker-compose up
```
or
```
docker-compose start
```


### Stopping containers
```
./stop
```
or

```
docker-compose stop
```

### Removing containers

To stop and remove all the containers use the`down` command:

```
docker-compose down
```

To Stops containers and removes containers, networks, volumes, and images created to the specific project
```
./kill
```
or

```
docker-compose down -v
```

### Creating database dumps

```
./export.sh
```

### WP CLI

The docker compose configuration also provides a service for using the [WordPress CLI](https://developer.wordpress.org/cli/commands/).

Sample command to install WordPress:

```
docker-compose run --rm wpcli core install --url=http://localhost --title=test --admin_user=admin --admin_email=test@example.com
```

Or to list installed plugins:

```
docker-compose run --rm wpcli plugin list
```

Or to search-replace:

```
docker-compose run --rm wpcli search-replace 'http://mysite.com' 'http://wp-app.local'
```
Create new admin user

```
docker-compose run --rm wpcli user create baracat baracat@example.com --role=administrator --user_pass=newpass
```

### For an easier usage you may consider adding an alias for the CLI:

```
alias wp="docker-compose run --rm wpcli"
```

This way you can use the CLI command above as follows:

```
wp plugin list
```

### phpMyAdmin

You can also visit `http://127.0.0.1:8080` to access phpMyAdmin after starting the containers.

The default username is `root`, and the password is the same as supplied in the `.env` file.

### License
This project is based in
[Harald Nezbeda](https://github.com/nezhar) docker environment: https://github.com/nezhar/wordpress-docker-compose
