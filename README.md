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
```php
<?php
require './vendor/autoload.php';

use Its\Sso\OpenIDConnectClient;
use Its\Sso\OpenIDConnectClientException;

try {
    $oidc = new OpenIDConnectClient(
                    'https://dev-my.its.ac.id', // authorization_endpoint
		    'XXXXXXX-XXXXXXX-XXXXXXX-XXXXXXX', // Client ID
		    '***********************' // Client Secret
		);
 
    $oidc->setRedirectURL('https://myweb.site/auth.php'); // must be the same as you registered
    $oidc->addScope('openid code phone profile'); //must be the same as you registered
    
    // remove this if in production mode
    $oidc->setVerifyHost(false);
    $oidc->setVerifyPeer(false);

    $oidc->authenticate(); //call the main function of myITS SSO login

    $_SESSION['id_token'] = $oidc->getIdToken(); // must be save for check session dan logout proccess
} catch (OpenIDConnectClientException $e) {
    echo $e->getMessage();
}
```

## Sample logout ##
```php
<?php
require './vendor/autoload.php';

use Its\OpenIDConnectClient;
use Its\OpenIDConnectClientException;

try {
    session_start();
    $redirect = 'https://myweb.site/index.php';

    if (isset($_SESSION['id_token'])) {
        $accessToken = $_SESSION['id_token'];

        session_destroy();

        $oidc = new OpenIDConnectClient(
                    'https://dev-my.its.ac.id', // authorization_endpoint
		    'XXXXXXX-XXXXXXX-XXXXXXX-XXXXXXX', // Client ID
		    '***********************' // Client Secret
		);
	
	// remove this if in production mode
	$oidc->setVerifyHost(false);
	$oidc->setVerifyPeer(false);

        $oidc->signOut($accessToken, $redirect);
    }

    header("Location: " . $redirect);
} catch (OpenIDConnectClientException $e) {
    echo $e->getMessage();
}
```
