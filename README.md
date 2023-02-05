# Simple Shopping Cart
![Firefox_Screenshot_2023-02-05T11-29-11 122Z](https://user-images.githubusercontent.com/65793636/216817853-adbe7e74-8644-49ea-bcea-541c3060bfe6.png)


## Packages Required:

- PHP 7.4.33
- Bootstrap 5.1.3
- Laravel-Mix 6.0.6
- Vue 2.6.12
- Vue-Loader 15.10.1
- Composer 2.4.4

### For running this app :
1. Make sure you have installed composer and node.js
2. Create an .env file based on the env.example file, run this command:

##### Windows
```
copy .env.example .env
```
##### Linux
```
    cp .env.example .env
```
3. Run this command in a command prompt or terminal for install the packages installed in composer
```
composer install
```
5. After successfully creating the .env file, then run the following command
```
php artisan key:generate
```
7. The last, you can run this app with this command
```
php artisan serve
```
