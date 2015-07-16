# How to install Laravel 
1. curl -s https://getcomposer.org/installer | php

The next code will be generating the Composer.Phar file (PHP executable) and run it.

2. php composer.phar

Next thing necessary is moving the .phar file to a place from where it will work at tandem with your local system.

3. sudo mv composer.phar /usr/local/bin/composer

Now it is time to move to create a Laravel project directly calling composer and it will do the rest of the part to build it calling and auto loading classes.  

It looks like this:

1. cd /var/www/html 
2. composer create-project laravel/laravel myproject --prefer-dist 

Finally it looks like this;


1. cd /var/www/html
2. laravel new myproject
