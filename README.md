# docker-compose for Laravel

## Project Structure

```
Project Name
├── dbdata
├── docker-compose.yml
├── Dockerfile
├── logs
│   └── nginx
├── nginx
│   └── conf.d
│       └── default.conf
├── README.md
└── src
```

## Usage
To get started, make sure you have Docker and Docker-compose installed on your system, and then clone this repository.

Add your entire Laravel project to the src folder. If you're creating a new project from scratch on Linux, make sure to run the composer container with your host's uid:gid combination to avoid permission problems

```docker-compose run --rm --user `id -u`:`id -g` composer create-project laravel/laravel .```

then from this cloned respository's root run ```docker-compose up -d --build```. Open up your browser of choice to http://localhost:3000 and you should see your Laravel app running as intended.

Containers have been added that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command templates from your project root, modifiying them to fit your particular use case:

* ```docker-compose run --rm composer update```
* ```docker-compose run --rm npm run dev```
* ```docker-compose run --rm artisan migrate```

### Frontend Setup for Laravel

The Bootstrap, Vue, and React scaffolding provided by Laravel is located in the laravel/ui Composer package, which may be installed using Composer:

 ```docker-compose run --rm --user `id -u`:`id -g` composer require laravel/ui```
 
Once the laravel/ui package has been installed, you may install the frontend scaffolding using the ui Artisan command:

```
// Generate basic scaffolding...
docker-compose run --rm --user `id -u`:`id -g` artisan ui bootstrap
docker-compose run --rm --user `id -u`:`id -g` artisan ui vue
docker-compose run --rm --user `id -u`:`id -g` artisan ui react

// Generate login / registration scaffolding...
docker-compose run --rm --user `id -u`:`id -g` artisan ui bootstrap --auth
docker-compose run --rm --user `id -u`:`id -g` artisan ui vue --auth
docker-compose run --rm --user `id -u`:`id -g` artisan ui react --auth
```

### Installing NPM Dependencies

Before compiling your CSS, install your project's frontend dependencies using the Node package manager (NPM):

```docker-compose run --rm npm install```

Once the dependencies have been installed using npm install, you can compile your SASS files to plain CSS using Laravel Mix. The npm run dev command will process the instructions in your webpack.mix.js file. Typically, your compiled CSS will be placed in the public/css directory:

```docker-compose run --rm npm run dev```

### Stack
* Nginx Stable (Alpine)
  * HOST:3000
* MySQL 8.0
  * HOST:3306
* PHP 7.4 FPM (Alpine)
  * HOST:9000
* PHPMyAdmin
  * HOST:8000
* Mailhog
  * HOST:8025
  * SMTP:1025
* Composer
* Node Current (Alpine)
* Artisan

### Notes for Usage
* .env
  * DB_HOST=db (Required)
  * MAIL_HOST=mail
  * MAIL_PORT=1025

#### For further documentation see the address below:

[https://laravel.com/docs/7.x](https://laravel.com/docs/7.x)