# Pece routing for Codeigniter 4 
### This library modifies the host for the URL helper and URI Service


## How to use in Routes:
There are new options in CI4 routing, you can use all or some

Example:
```
$routes->get('/test/(:any)', 'Test::index/$1', ['pSubdomain'=> '[a-z]+', 'pDomain'=>'ci.loc', 'pSSL' => null, 'pSubhost' => false]);
```

#### Limit to subdomain:

When the subdomain option is present, the system will restrict the routes to only be available on that sub-domain. The route will only be matched if the subdomain is the one the application is being viewed through:

Regular Expressions
If you prefer you can use regular expressions to define your subdomain rules. Any valid regular expression is allowed

Example: 
```
// Limit to media.example.com
$routes->add('from', 'to', ['pSubdomain' => 'media']); or
$routes->add('from', 'to', ['pSubdomain' => '[a-z]+']);
```

#### Limit to Domain
You can restrict groups of routes to function only in certain domain of your application by passing the “pDomain” option along with the desired domain to allow it on as part of the options array:
Example:
```
$routes->get('from', 'to', ['pDomain' => 'example.com']);
```

#### Limit to SSL
If you need limiting to https use true, to http set false or not limiting set null
Example:
```
$routes->get('from', 'to', ['pSSL' => true]);
```

#### Setting subdomain+domain as host
if you want to use subdomain and domain as host in CI4 set this option as true or false with otherwise
Example:
```
$routes->get('from', 'to', ['pSubhost' => true]);
```



## How to use in your app e.g. controller:
Change host from subdomain to domain:
`Services::pece()->setDomainInCI();`
>xxx.host.com => host.com

Change host from domain to subdomain (if the request is from a subdomain, reverse `setDomainInCI()`):
`Services::pece()->setSubdomainInCI();`
>host.com => xxx.host.com

Change subdomain in host:
`Services::pece()->changeSubdomainInCI('new.sub.domain');`
>host.com => new.sub.domain.host.com<br>
>abc.host.com => new.sub.domain.host.com


Add to subdomain in host
`Services::pece()->addSubdomainInCI('new.sub.domain');`
>host.com => new.sub.domain.host.com<br>
>abc.host.com => new.sub.abc.domain.host.com


Other methods:
```
Services::pece()->
getDomain(): - return request domain
getSubdomain(): - request subdomain
getScheme(): - request scheme e.g. 'https://' or 'http://'
```


## Instalation:

- Composer
```
composer require szajens/pece
```
