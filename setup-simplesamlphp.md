# SAML with SimpleSAMLphp


### Server setup

ensure php-gmp is installed
```
sudo apt install php-gmp
```


### Download and install SimpleSAMLphp

The most recent release of SimpleSAMLphp is found at https://simplesamlphp.org/download.

Go to the directory where you want to install SimpleSAMLphp, and extract the archive file you just downloaded:
```
cd /var
tar xzf simplesamlphp-1.x.y.tar.gz
mv simplesamlphp-1.x.y simplesamlphp
```

## Installing

see https://simplesamlphp.org/docs/stable/simplesamlphp-install


### Configuring Apache


Ensure the saml vhost has the following:

```
<VirtualHost *:80>
  ServerName saml.test.dev

  SetEnv SIMPLESAMLPHP_CONFIG_DIR /vagrant/www/projects/simplesamlphp/config
  Alias /simplesaml /vagrant/www/projects/simplesamlphp/www

  ## Vhost docroot
  DocumentRoot "/vagrant/www/projects/simplesamlphp/www"

  ...
```


### SimpleSAMLphp configuration: config.php

There is a few steps that you should edit in the main configuration file, config.php, right away:

**1) Password**

Set a administrator password. This is needed to access some of the pages in your SimpleSAMLphp installation web interface.
```
'auth.adminpassword'        => 'setnewpasswordhere',
```

Hashed passwords can also be used here. See the authcrypt documentation for more information.

**2) Salt**

Set a secret salt. This should be a random string. Some parts of the SimpleSAMLphp needs this salt to generate cryptographically secure hashes. SimpleSAMLphp will give an error if the salt is not changed from the default value. The command below can help you to generated a random string on (some) unix systems:
```
tr -c -d '0123456789abcdefghijklmnopqrstuvwxyz' </dev/urandom | dd bs=32 count=1 2>/dev/null;echo
```
Here is an example of the config option:
```
'secretsalt' => 'randombytesinsertedhere',
```

**3) Contact (optional)**

Set technical contact information. This information will be available in the generated metadata. The e-mail address will also be used for receiving error reports sent automatically by SimpleSAMLphp. Here is an example:
```
'technicalcontact_name'     => 'John Doe',
'technicalcontact_email'    => 'john@google.com',
```
If you use SimpleSAMLphp in a country where English is not widespread, you may want to change the default language from English to something else:


**4) Timezone (optional)**
Set the timezone which you use:
```
'timezone' => 'UTC',
```


### update composer packages
```
cd /vagrant/www/projects/simplesamlphp
composer install
```



