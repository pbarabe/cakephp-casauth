# CAS Authentication for CakePHP 4.x

Very basic CAS Authentication for CakePHP 4.

## Installing via composer

Install into your project using [composer](http://getcomposer.org).
For existing applications you can add the following to your composer.json file:

```json
    "repositories": [
      {
        "type": "git",
        "url": "https://github.com/uazgraduatecollege/cakephp-casauth.git"
      }
    ],
    "require": {
        "uazgraduatecollege/cakephp-casauth": "~2.0"
    }
```

And run `php composer.phar update`

## Usage

Load the Cake AuthComponent, including CasAuth.Cas as an authenticator.
For example:

```php
$this->loadComponent('Auth');

$this->Auth->config(
    'authenticate',
    [
        'CasAuth.Cas' => [
            'cas_host => 'cas.mydomain.com',
            'cas_context => '/cas,
            'client_service_name => 'https://clientapplication.otherdomain.com',
        ]
    ]
);
```

Or combine the load and configuration into one step:

```php
$this->loadComponent(
    'Auth',
    [
        'authenticate' => [
            'CasAuth.Cas' => [
                'cas_host => 'cas.mydomain.com',
                'cas_context => '/cas,
                'client_service_name => 'https://clientapplication.otherdomain.com',
            ]
        ]
    ]
);

```

## Parameters

* **cas_host** is required.
* **cas_context** defaults to '' (an empty string)
* *client_service_name* (optional) defaults to `$_SERVER['SERVER_NAME']`
* *cas_port* defaults to 443
* *debug* (optional) if true, then phpCAS will write debug info to your configured logger.
* *cert_path* (optional) if set, then phpCAS will use the specified CA certificate file to verify the CAS server
* *curlopts* (optional) key/value paired array of additional CURL parameters to pass through to phpCAS::setExtraCurlOption, e.g.

```php
'curlopts' => [CURLOPT_PROXY => 'http://proxy:5543', CURLOPT_CRLF => true]
```

### Note about parameter key changes

Prior to release 2.0.0, several parameter used different keys.
Release 2.0.0 updates `apereo/phpcas` to use at least version 1.6, which contains breaking changes.
For better clarity, the previous parameter key names have been re-mapped to the new names, which
match variable names as used in the `apereo/phpcas`
[example client usage](https://github.com/apereo/phpCAS/blob/master/docs/examples/example_simple.php).

- `hostname` changed to `cas_host`
- `port` changed to `cas_port
- `uri` changed to `cas_context`

cakephp-casauth looks for input parameters using the old keys to try to remain backwards compatible.
Your mileage may vary.

## License

This project was forked from
[Glen Sawyer's cakephp-3-cas repository](https://github.com/snelg/cakephp-3-cas)
and retains the original Apache License version 2.0.

