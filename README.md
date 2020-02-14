PHP OpenID Connect Basic Client
========================
A simple library that allows an application to authenticate a user through the basic OpenID Connect flow.
This library hopes to encourage OpenID Connect use by making it simple enough for a developer with little knowledge of
the OpenID Connect protocol to setup authentication.

developed specifically to connect applications that want to connect with myITS SSO.

# Prerequisite #
Your application must be registered to the system, you can register your app by visit DPTSI-ITS and ask for registrating your app

# Requirements #
 1. PHP 5.4 or greater
 2. phpseclib/phpseclib 2.0 or greater
 3. CURL extension
 4. JSON extension

## Install ##
 1. Install library using composer
```
composer require myits/openid-connect-client
```
 2. Include composer autoloader and use class OpenIDConnectClient
```php
require __DIR__ . '/vendor/autoload.php';

use Its\Sso\OpenIDConnectClient;
use Its\Sso\OpenIDConnectClientException;
```
## Sample login ##
```
<?php
use Its\Sso\OpenIDConnectClient;
use Its\Sso\OpenIDConnectClientException;

try {
 $oidc = new OpenIDConnectClient(
  'https://my.its.ac.id', // authorization_endpoint
  '849D9D71-D0D5-408B-A89B-A76D912687CF', // Client ID
  '00b53ea23741cf2eeafb4f9c' // Client Secret
 );
 
 $oidc->setRedirectURL('https://php-client-1.local/auth.php'); // must be the same as you registered
 $oidc->addScope('openid code phone profile'); //must be the same as you registered

 $oidc->authenticate(); //call the main function of myITS SSO login

 $_SESSION['id_token'] = $oidc->getIdToken(); // must be save for check session dan logout proccess
} catch (OpenIDConnectClientException $e) {
	echo $e->getMessage();
}
```
