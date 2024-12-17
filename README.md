
# bts-projectコーディング規約
### このドキュメントの目的
1. コード品質の安定<br>
    ・メンバー全員がある一定以上の品質でコーディングできること。
2. コミュニケーションコストの削減<br>
    ・メンバー間の連絡や質問事項を減らすこと。
3. 経験から得られる注意事項の共有<br>
    ・一度学んだことをメンバー間で共有すること。
    

## 全体で共通の規約
・文字コードは UTF-8（BOM無し）を使用すること。<br>
・文字列を定義する場合は、ダブルコーテーション「""」を使用し、必要に応じてシングルコーテーションを使用すること。

## Laravel<br>
・コーディング規約はPSR-2/PSR-4に従うこと。<br>
https://laravel.com/docs/master/contributions#coding-style

| 規約 | 詳細(日本語) | 詳細(原文) |
| ------------- | ------------- | ------------- |
| PSR2(コーディングスタイル) | [日本語サイト](http://www.infiniteloop.co.jp/docs/psr/psr-2-coding-style-guide.html)| [原文サイト](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) |
| PSR4(オートローディング規約)| [日本語サイト](https://www.ritolab.com/entry/96) | [原文サイト](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) |


・PHPだけが書かれたファイルについて、PHPタグは <?php を使用し、閉じタグは省略すること。<br>
・全てのPHPファイルは、最後に空行を入れること。<br>
・１ファイルにつき１クラスを定義すること。<br>
・インデントは半角スペース4つで行うこと。<br>
・PHPの定数「true」「false」「null」、PHPの[キーワード](https://www.php.net/manual/ja/reserved.keywords.php)は小文字で記述すること。

・ExtendsとImplementsは、クラス名と同じ行に定義すること。
```
<?php
class ClassName extends ParentClass implements SomethingInterface
{
    // constants, properties, methods
}
```
#### プロパティ
・1つのステートメントで2つ以上のプロパティは定義しないこと。
```
class SampleClass
{
  public $foo,$bar;  // ←この書き方はNG
  public $foo;
  private $bar;
  protected $haystack;
}
```
#### メソッド
・メソッド名の後ろにはスペースを入れないこと。<br>
・開始/終了波括弧は単体それのみで１行に記述すること。<br>
・開始括弧の後ろにはスペースを入れないこと。<br>
・閉じ括弧の前にはスペースを入れないこと。<br>
・引数を記述する際、カンマの前にスペースを入れないこと。カンマの後にはスペースを1つ入れること。<br>
・デフォルト値を持つメソッド引数は最後に記述すること。
```
class SampleController
{
    public function index($arg1, $arg2, default=null)
    {

    }
```

### 制御構文
・入れ子は最大でも３段階(推奨２段階まで)とすること。<br>
・インデックス(カウンタ)として使う変数は、i, j, k を使うこと。その際、一番外側のループから順に i, j, k とすること。

・括弧、スペースの位置は、下記例を参考にすること。

#### if/elseif/else文
```
<?php

if ($foo) {
  
} elseif ($bar) {
  
} else {
  
}
```
#### switch/case文
```
<?php

switch ($hoge) {
    case 0:
        echo '通常パターン。breakします。';
        break;
    case 1:
        echo 'no breakパターン。処理は継続されます。';
    // no break
    case 2:
    case 3:
    case 4:
        echo 'returnパターン, breakの代わりにreturnします。';
        return;
    default:
        echo 'Default case';
        break;
}
```
#### while/do while文
```
<?php

while ($expr) {
    // structure body
}

do {
    // structure body;
} while ($expr);
```
#### for文
```
<?php

for ($i = 0; $i < 10; $i++) {
    // for body
}
```

#### foreach文
```
<?php

foreach ($iterable as $key => $value) {
    // foreach body
}
```
#### try catch文
```
<?php

try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
#### Closure
```
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
 
### 名前空間とuse演算子
・名前空間の定義の後に空行を入れること。<br>
・use定義は、名前空間宣言の後に記述すること。<br>
・定義ごとにuse演算子を記述すること。<br>
・use定義のブロックの後には空行を入れること。
```
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

### 静的解析ツール
PSRに基づいたコーディングを容易にする為、下記PHP-CS-Fixerを導入すること。

##### PHP-CS-Fixer 導入手順
[日本語サイト](https://qiita.com/suin/items/4242aec018d086312fe7)
[原文サイト](https://cs.symfony.com/)
 ※原則デフォルト設定とし、必要に応じてカスタマイズを行うこと。[(カスタマイズ参考)](https://qiita.com/ryoichi-u/items/af10768d6adc5de389e7)
 
### 命名規約

・各種名前は、下記記法に従うこと

| 種類 | 記法 | 複数or単数 | 例 | 備考 |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| テーブル名 | スネークケース | 複数 | posts<br>client_users | ------------- |
| モデル名  | アッパーキャメル  | 単数 | Post.php<br>ClientUser.php | テーブル名に合わせること |
| migration名  | スネークケース  | 複数 | xxx_create_posts_table<br>xxx_create_client_users_table | ------------- |
| seeder名  | アッパーキャメル  | 指定なし | PostsSeeder<br>ClientUserSeeder | ------------- |
| Controllers名  | アッパーキャメル  | 単数 | PostController.php<br>ClientUserController.php | ------------- |
| クラス名 | アッパーキャメル | 単数 | PostController<br>ClientUserController | Controllers名に合わせること |
| views名  | スネークケース  | 指定なし | posts.blade.php<br>client_user.blade.php | ------------- |
| メソッド名  | ローワーキャメル  | 指定なし | getAll<br>editUserName | ------------- |
| 変数名  | スネークケース  | 指定なし | $post_id<br>$client_users_name | ------------- |

・名前は、英単語を使用すること。[ネーミング辞書](https://codic.jp/)<br>
・１文字または２文字など短い変数名を使用する場合は、メソッド内のみで使用すること。

・名前の長さ<br>
スネークケースでは、アンダーバー( _ )『5個』以内とすること。<br>
ローワーキャメルでは、英大文字『5個』以内とすること。<br>
アッパーキャメルでは、英大文字『6』個以内とすること。

・変数名に関しては、略語が一般的なものはその慣例に従っても良いこと<br>
```
例)
$average → $avg
$Monday  → $Mon
$number  → $no
```

・複数の動作が想定される単語は避け、理解できる具体的な名前を使い、内容を詳細に説明すること。<br>
[英単語まとめ](https://qiita.com/Ted-HM/items/7dde25dcffae4cdc7923)<br>


### 禁止事項<br>
保留(使ってはいけない文法など)

### 制限事項<br>
保留(推奨されない機能、コーディング方法、クラスなど)

### その他<br>
・実装/修正予定の箇所には@Todoでコメントアウトすること。


## HTML(Blade), CSS<br>
・JSとCSSをBladeテンプレートの中に入れないこと。<br>
・PHPクラスの中にHTMLを入れないこと。

## SQL<br>
・クエリビルダや生のSQLクエリよりもEloquentを優先して使い、配列よりもコレクションを優先すること。<br>
・Bladeテンプレート内でクエリを実行しないこと。




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
