PHP OpenID Connect Basic Client
========================
A simple library that allows an application to authenticate a user through the basic OpenID Connect flow.
This library hopes to encourage OpenID Connect use by making it simple enough for a developer with little knowledge of
the OpenID Connect protocol to setup authentication.

developed specifically to connect applications that want to connect with myITS SSO.

# Requirements #
 1. PHP 5.4 or greater
 2. phpseclib/phpseclib 2.0 or greater
 3. CURL extension
 4. JSON extension

## Install ##
 1. Install library using composer
```
composer require myits/openid-connect-php
```
 2. Include composer autoloader
```php
require __DIR__ . '/vendor/autoload.php';
```