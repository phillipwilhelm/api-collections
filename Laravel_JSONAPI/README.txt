# About
Laravel JSON:API is backend product built by [Creative Tim](https://www.creative-tim.com/) and [UPDIVISION](https://updivision.com/).
To find out more about the project visit our [product page](https://www.creative-tim.com/product/vue-material-dashboard-laravel-pro).

# JSON:API
JSON:API is a specification for how a client should request that resources be fetched or modified, and how a server should respond to those requests. 
It is designed to minimize both the number of requests and the amount of data transmitted between clients and servers. This efficiency is achieved without compromising readability, flexibility, or discoverability.

# Prerequisites

The Laravel JSON:API backend project requires a working Apache/Nginx local environment with PHP, Composer and MySQL.

If you don't already have a local development environment, use one of the following links:
- Windows: [How to install WAMP on Windows](https://updivision.com/blog/post/beginner-s-guide-to-setting-up-your-local-development-environment-on-windows)
- Linux: [How to install LAMP on Linux](https://howtoubuntu.org/how-to-install-lamp-on-ubuntu)
- Mac: [How to install MAMP on MAC](https://wpshout.com/quick-guides/how-to-install-mamp-on-your-mac/)
- Install Composer: [https://getcomposer.org/doc/00-intro.md](https://getcomposer.org/doc/00-intro.md)

Install Composer: https://getcomposer.org/doc/00-intro.md

# Download
For the free version of the project you can either
- download the .zip file from the Creative Tim site and extract it or
- make a clone from the Github repository
For the PRO version you will download the .zip file after you purchase the product on the [Creative Tim](https://www.creative-tim.com/) website.

Unzip the archie and you will get two project folders: one for the Laravel API project and one for the Vue frontend.

# Installation
1. Navigate in your Laravel API project folder: `cd your-laravel-json-api-project`
2. Install project dependencies: `composer install`
3. Create a new .env file: `cp .env.example .env`
3. Add your own database credentials in the .env file in DB_DATABASE, DB_USERNAME, DB_PASSWORD
5. Create users table: `php artisan migrate --seed`
6. Generate application key: `php artisan key:generate`
7. Install Laravel Passport: `php artisan passport:install`
8. Add your own mailtrap.io credentials in MAIL_USERNAME and MAIL_PASSWORD in the .env file
