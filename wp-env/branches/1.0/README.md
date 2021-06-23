# Pollen Wordpress Env Component

[![Latest Version](https://img.shields.io/badge/release-1.0.0-blue?style=for-the-badge)](https://www.presstify.com/pollen-solutions/asset/)
[![MIT Licensed](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)](LICENSE.md)
[![PHP Supported Versions](https://img.shields.io/badge/PHP->=7.4-8892BF?style=for-the-badge&logo=php)](https://www.php.net/supported-versions.php)

Pollen **Wordpress Env** Component provides a simply solution to configure your Wordpress with .env file.

## Installation

```bash
composer require pollen-solutions/wp-env
```

## Configuration

### .env config file

Create a .env file at the root of your project :

```dotenv
# ENVIRONMENT CONFIGURATION
## Environnement of your application. 
## dev|prod. 
APP_ENV=dev
## Enabling debug
APP_DEBUG=true
## Url of your application
APP_URL=https://127.0.0.1:8000
## Application timezone
APP_TIMEZONE=Europe/Paris

# PATHS CONFIGURATION
## Relative public path of your application 
APP_PUBLIC_DIR=/
## Relative path to the wordpress root folder, containing wp-admin and wp-includes folder 
APP_WP_DIR=/
## Relative path to the wp-content root folder, containing languages, themes, uploads ...
## MUST BE WRITABLE BY HTTP SERVER 
APP_WP_PUBLIC_DIR=wp-content

# DATABASE CONNEXION
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=wordpress
DB_USERNAME=root
DB_PASSWORD=
DB_PREFIX=wp_

# WORDPRESS CONFIGURATION
# @see https://wordpress.org/support/article/editing-wp-config-php/
WP_DEBUG_LOG=true
DISALLOW_FILE_MODS=true
AUTOMATIC_UPDATER_DISABLED=false
DISABLE_WP_CRON=false

## WORDPRESS SALT
## @see https://developer.wordpress.org/reference/functions/wp_salt/
## @see https://api.wordpress.org/secret-key/1.1/salt/
## Generate with :
## php vendor/bin/wp-salt dotenv --clean >> .env
AUTH_KEY="r?J}leh:s)W-hjIoLb]lD)#],@w8b{#*|8>bc](k~ds!izz~J*phqE[[!B_(9nPl"
SECURE_AUTH_KEY="r]xS1)5?uHY@OM]7%V7[O-Gh2<SL~bzx/01j2W)Pa]c!}x3sm,rmO?[}H^uo`hu."
LOGGED_IN_KEY="M/9^coIb%b~n~kNWws/u[?8a_%r!&AA]+(s?_D3v8RgK2f)FOHI&u,)T?)fRp<9i"
NONCE_KEY="?Q/-+]yh]ttgdflzqb-$Ln)JN*h![01L+$x~`uNw5FDnR=:Sa}purf%1[?0Gw0We"
AUTH_SALT="GfNy(G07G4drvcW|K]s|%&`1RA~.y}3>#mlox<Fx~Mp>TCliw!mI`kzp<?PI.U#s"
SECURE_AUTH_SALT="^v&;6zay$eK*yjA|p|^.autQ>gylaWE>*,ZUDdDQlj0>nu}@PjSl{vO|A,Sb.176"
LOGGED_IN_SALT="T)JFGirExD|n%8yh9];XhFAqL}-{vbJxnoE?>)E%(]O+sYo|os9^~Q{&(<6mGD7P"
NONCE_SALT="Q:PD/},=:d0JK){-xT;NnTxhk+g*s&(ay#91y98quymCp&Q~;m*i.&-Oo`9UzXDz"
```

### Edit wp-config.php

Replace the contents of wp-config.php file with the code below :

```php
use Pollen\WpEnv\WpEnv;

defined('START_TIME') ?: define('START_TIME', microtime(true));

require_once __DIR__ . '/vendor/autoload.php';

new WpEnv(__DIR__);
```


