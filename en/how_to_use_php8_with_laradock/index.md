# How to use PHP8 with Laradock


Hello, it is me again. I use laradock to host all my test projects. And today I want some projects to use PHP 7.4 and some projects will use 8.0. I use Ubuntu 20.04 to test. Have fun.

First of all please remember that it is very important to **backup** your configuration file: **docker-compose.yml**.

Now, edit your files: **docker-compose.yml** and **.env**

**.env**
```bash
…
#PHP 8 version
PHP8_VERSION=8.0
…
#Define some new ports to difference from original workspace
WORKSPACE_PHP8_SSH_PORT=2223
WORKSPACE_PHP8_BROWSERSYNC_HOST_PORT=4000
WORKSPACE_PHP8_BROWSERSYNC_UI_HOST_PORT=4001
WORKSPACE_PHP8_VUE_CLI_SERVE_HOST_PORT=9080
WORKSPACE_PHP8_VUE_CLI_UI_HOST_PORT=9001
WORKSPACE_PHP8_ANGULAR_CLI_SERVE_HOST_PORT=5200

```
<!--more-->
**docker-compose.yml**
- Copy **workspace** entry and rename to **workspace-php-8**
- Inside **workspace-php-8** entry:
```bash
#PHP8 version
- LARADOCK_PHP_VERSION=${PHP8_VERSION}
…
#Does not work with PHP8
- INSTALL_XDEBUG=false
…
#Does not work with PHP8
- INSTALL_IMAGEMAGICK=false
…
#Does not work with PHP8
- INSTALL_AST=false
…
#Change some ports to difference from php_workspace
ports:
    - "${WORKSPACE_PHP8_SSH_PORT}:22"
    - "${WORKSPACE_PHP8_BROWSERSYNC_HOST_PORT}:3000"
    - "${WORKSPACE_PHP8_BROWSERSYNC_UI_HOST_PORT}:3001"
    - "${WORKSPACE_PHP8_VUE_CLI_SERVE_HOST_PORT}:8080"
    - "${WORKSPACE_PHP8_VUE_CLI_UI_HOST_PORT}:8000"
    - "${WORKSPACE_PHP8_ANGULAR_CLI_SERVE_HOST_PORT}:4200"
```

- Copy **php-fpm** entry and rename to **php8-fpm**
Inside **php8-fpm** entry:
```bash
#PHP version 8
- LARADOCK_PHP_VERSION=${PHP8_VERSION}
…
#Does not work with PHP8
- INSTALL_XDEBUG=false
…
#Does not work with PHP8
- INSTALL_IMAGEMAGICK=false

…
ports:
  - "9004:9003"

…
depends_on:
  - workspace-php-8
```

- Run new container
```bash
docker-compose up -d workspace-php-8 php8-fpm
```
- Waitting for build and up.
- Access workspace-php-8 and check php version
```bash
docker-compose exec workspace-php-8 bash
#Inside docker container
php -v
```
- Access php8-fpm and check php version
```bash
docker-compose exec php8-fpm bash
#Inside docker container
php -v
```

- Configure your site to work with php 8
Inside your site’s nginx configuration file:
```bash
…
fastcgi_pass php8-fpm:9000;
….
```

