# nttdata-movie
NTTDATA TEST

## Prerequisites
![Lando](https://github.com/lando/lando/releases/tag/v3.0.0-rc.20)

## Installation
In order to initiate the Lando stack, run
```
$ lando start
```
which will create the following containers: appserver (Nginx + PHP), database

#### Importing the initial database with Lightning
Download the latest database from our project's Google Drive and run
```
$ lando db-import <filename>
```

#### Installing Composer dependencies
```
$ cd www && lando composer install
```

#### Setting up the website
```
$ cd docroot/sites/default
```

Create a settings.php (mandatory file for Drupal installations) on
www/docroot/sites/default by copying the default one from
[drupal.org]

##### Add the following database pointing at the end of it:
```
$databases['default']['default'] = array (
  'database' => 'drupal9',
  'username' => 'drupal9',
  'password' => 'drupal9',
  'prefix' => '',
  'host' => 'database',
  'port' => '3306',
  'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
  'driver' => 'mysql',
);
```

##### Include the configuration path as well:
```
$config_directories['sync'] = 'config/sync';
```

#### Importing the configuration
Get back to docroot directory and import the configuration with
```
$ lando drush cim -y
```

## Login
In order to login, usually the one-time login URL is used:
```
$ drush -l https://https://movies-app.lndo.site uli
```
Also, feel free to update the admin password with it and login through "/user".

## General development
Please follow Drupal usual workflow/strategy. Also, keep in mind that Lando
mimics the folder you're currently running any command, so drush should be used
inside "www/docroot".\
**@TODO**: it might be a good idea to extend it (if possible) and make drush run on
every path (something like we did for "theme" - check .lando.yml and script.sh).

## Theme development
custom bootstrap_barrio generate cli

