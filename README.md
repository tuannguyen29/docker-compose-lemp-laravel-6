
## LARAVEL - DOCKER COMPOSE LEMP PROJECT

Configuration for DEV environment of Laravel project with Docker Container.
- Nginx
- PHP 7.2
- Mysql 5.7
- Laravel 6.0.3
- Redis Cache 3.0

### Prerequisite
You must install docker to able to do things with below guidelines (see https://docs.docker.com/install/)

### Let's checkout source_code and run below command to get started

* Docker up:
Run file `./start-docker-compose.sh` or change directory:
        `cd docker`
        `docker-compose up --build`
- Then, run the next time, just:
        `docker-compose up -d`
* Docker stop:
Run file `./stop-docker-compose.sh`
* Initializing configuration Laravel:
```
	$ cd docker
    $ docker-compose exec app bash
    $ cp .env.example .env
    $ composer install
    $ php artisan key:generate
```
* Migrate database:
Edit  `/var/www/.env`
```		
DB_CONNECTION=mysql
DB_HOST=your_server_ip
DB_PORT=53306
DB_DATABASE=develop_ntdev_blog
DB_USERNAME=root
DB_PASSWORD=ntdev@123
```
Run migration:
	
		$  php artisan migrate

Result:

	Migration table created successfully.
	Migrating: 2014_10_12_000000_create_users_table
	Migrated:  2014_10_12_000000_create_users_table (0.03 seconds)
	Migrating: 2014_10_12_100000_create_password_resets_table
	Migrated:  2014_10_12_100000_create_password_resets_table (0.02 seconds)
	Migrating: 2019_08_19_000000_create_failed_jobs_table
	Migrated:  2019_08_19_000000_create_failed_jobs_table (0.01 seconds)


* Using an `/etc/hosts` file for custom domains during development
* OPEN `/etc/hosts` (MAC) or %windir%\system32\drivers\etc\hosts (Windows) and type:
`127.0.0.1 localhost`

### That's it. Let's go into some interesting information!
* How to check the webpages are running ok or not? Try it

        http://your_server_ip

* How to see which services are running? Run it:
        
        $ docker-compose ps

### Remote MySQL
```
DB_HOST: 127.0.0.1 (or your IP address)
DB_PORT: 53306
DB_DATABASE: develop_ntdev_blog
DB_USERNAME: root (or user)
DB_PASSWORD: ntdev@123 (or user)
```
### Run PHPUnit
```
./vendor/phpunit/phpunit/phpunit
```
Result:
```
PHPUnit 8.3.5 by Sebastian Bergmann and contributors.

..                                                                  2 / 2 (100%)

Time: 2.72 seconds, Memory: 16.00 MB

OK (2 tests, 2 assertions)
```
**Notes**:
After installing Laravel, you may need to configure some permissions. Directories within the  `storage` and the `bootstrap/cache` directories should be writable by your web server or Laravel will not run.
