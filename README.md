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
## Generate salt from cli :
## php vendor/bin/wp-salt dotenv --clean >> .env
```

### Edit wp-config.php

Replace the contents of wp-config.php file with the code below :

```php
use Pollen\WpEnv\WpEnv;

// Optionnal but recommended start time global indicator
defined('START_TIME') ?: define('START_TIME', microtime(true));

require_once __DIR__ . '/vendor/autoload.php';

new WpEnv(__DIR__);

require_once(ABSPATH . 'wp-settings.php');
```


