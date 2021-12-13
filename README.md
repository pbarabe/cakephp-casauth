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
        "uazgraduatecollege/cakephp-casauth": "~1.0"
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
            'hostname' => 'cas.mydomain.com',
            'uri' => 'authpath'
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
                'hostname' => 'cas.mydomain.com',
                'uri' => 'authpath'
            ]
        ]
    ]
);

```

CAS parameters can be specified during `Auth->config` as above,
or by writing to the "CAS" key in Configure::write, e.g.
```php
Configure::write('CAS.hostname', 'cas.myhost.com');
Configure::write('CAS.port', 8443);
```

## Parameters

* **hostname** is required
* **port** defaults to 443
* **uri** defaults to '' (an empty string)
* *debug* (optional) if true, then phpCAS will write debug info to logs/phpCAS.log
* *cert_path* (optional) if set, then phpCAS will use the specified CA certificate file to verify the CAS server
* *curlopts* (optional) key/value paired array of additional CURL parameters to pass through to phpCAS::setExtraCurlOption, e.g.
```php
'curlopts' => [CURLOPT_PROXY => 'http://proxy:5543', CURLOPT_CRLF => true]
```

## License

This project was forked from
[Glen Sawyer's cakephp-3-cas repository](https://github.com/snelg/cakephp-3-cas)
and retains the original Apache License version 2.0.

