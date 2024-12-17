# bts-project
## 🚀 Local Development Environment

```
PHP 7.4.8
Composer 1.10.9
laravel 6.9

[Docker]
mariadb 10.5.4
redis 6.0.5
```

## 🛠️ How To SetUp
```
brew install php@7.4
brew install redis

git clone https://github.com/Kohei-Genchi/sample-bts-project.git
---------------
※Edit .env File
※Edit database.php
※Edit session.php
---------------
cd bts-project
docker-composer up -d
cd src
composer update
php artisan migrate
php artisan db:seed 
## 🔒 TestAccount
name	password	Auth
system	system	1
admin	admin	2
user	user	3
customer	customer	4
```
## 📚 Reference
```
php artisan make:model Company
php artisan make:migration create_companies_table
php artisan make:factory CompanyFactory
php artisan make:seeder CompanyTableSeeder

//Edit xxx_create_companies_table.php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateCompaniesTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('companies', function (Blueprint $table) {
            $table->bigIncrements('company_id');
            $table->integer('users_id');
            $table->String('company_name');
            $table->string('company_password');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('company');
    }
}

//Edit CompanyTableSeeder.php
<?php

use Illuminate\Database\Seeder;
use App\Repositories\Models\Company;

class CompanyTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        factory(Company::class, 10)->create();
    }
}

//Edit CompanyFactory.php
<?php

/** @var \Illuminate\Database\Eloquent\Factory $factory */

use App\Repositories\Models\Company;
use Faker\Generator as Faker;

$factory->define(Company::class, function (Faker $faker) {
    return [
        'users_id' => $faker->numberBetween($min = 1, $max = 10000),
        'company_name' => $faker->company,
        'company_password'=>$faker->password,
        'created_at' => $faker->datetime($max = 'now', $timezone = date_default_timezone_get()),
        'updated_at' => $faker->datetime($max = 'now', $timezone = date_default_timezone_get()),
    ];
});


//Edit DatabaseSeeder.php
php artisan migrate
php artisan db:seed
```

## TDD
```
@phpunit
@php artisan dusk
@cat storage/logs/laravel.log
@RefreshDatabaseとDatabaseMigrations
Edit phpunit.xml
<testsuite name="Browser">
            <directory suffix="Test.php">./tests/Browser</directory>
</testsuite>

1.Edit web.php
2.php artisan make:test TaskControllerTest
rm -rf tests/Feature/ExampleTest.php
rm -rf tests/Unit/ExampleTest.php
3.Edit TaskControllerTest.php
4.php artisan make:controller TaskController
5.Edit TaskController.php
6.php artisan make:model Task -m
7.Edit Task.php  //protected $filable=[];
8.Edit xxx_create_tasks_table.php
9.php artisan make:seeder TasksTableSeeder
10.Edit TasksTableSeeder.php
11.Edit DatabaseSeeder.php
12.composer dump-autoload
13.php artisan migrate --env=testing --seed
14.php artisan make:test TaskTest --unit
15.touch resources/views/tasks/index.blade.php
//VueFile
composer require --dev laravel/dusk:"^2.0"
php artisan dusk:install
rm -rf tests/Browser/ExampleTest.php
16.Edit DuskTestCase.php
$options = (new ChromeOptions)->addArguments([
            '--disable-gpu',
            '--headless',
            '--lang=ja_JP'
        ]);
17.php artisan dusk:make TasksIndexTest
18.Edit TasksIndexTest.php
19.Edit TaskController.php

composer require "laravelcollective/html":"^5.4.0"
Edit config/app.php
Collective\Html\HtmlServiceProvider::class,
(略)
        'Form' => Collective\Html\FormFacade::class,
        'Html' => Collective\Html\HtmlFacade::class,
        
```
## Have to do
```
CREATE DATABASE DATABASE-NAME;
※Edit database.php
'default' => env('DATABASE-NAME','DATABASE-NAME' ),   //作成後、'default' => env('DB_CONNECTION', 'mysql'),に戻す

'connections' => [
        'DATABASE-NAME' => [
            'driver' => 'mysql',
            'url' => env('DATABASE_URL'),
            'host' => env('127.0.0.1', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('Grady_GrouCp', 'Grady_GrouCp'),
            'username' => env('DB_USERNAME', 'forge'),
            'password' => env('DB_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => 'utf8mb4',
            'collation' => 'utf8mb4_unicode_ci',
            'prefix' => '',
            'prefix_indexes' => true,
            'strict' => true,
            'engine' => null,
            'options' => extension_loaded('pdo_mysql') ? array_filter([
                PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
            ]) : [],
        ],
    ],

```
php artisan migrate<br>
php artisan db:seed --class=ClientTableSeeder<br>
php artisan db:seed --class=UserTableSeeder
