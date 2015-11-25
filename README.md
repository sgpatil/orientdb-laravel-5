
# Orientdb Driver for Laravel 5


Orientdb Graph Eloquent Driver for Laravel 5

## Quick Reference

 - [Requirements](#requirements)
 - [Installation](#installation)
 - [Configuration](#Database Configuration)
 - [Migration](#migration)
 - [Relationships](#relationships)

## Requirements
   * Laravel 5.1 or above
   * Orientdb Server 2.1 or above

## Installation

Add the package to your `composer.json` and run `composer update`.

```json
{
    "require": {
        "sgpatil/orientdb-laravel-5": "dev-master"
    }
}
```

Add the service provider in `config/app.php`:

```php
Sgpatil\Orientdb\OrientdbServiceProvider::class,
```

This will register all the required classes for this package.

## Database Configuration

Open `config/database.php`
make `orientdb` your default connection:

```php
'default' => 'orientdb',
```

Add the connection defaults:

```php
'connections' => [
    'orientdb' => [
        'driver' => 'orientdb',
        'host'   => 'localhost',
        'port'   => '2480',
        'database' => 'database_name',
        'username' => 'root',
        'password' => 'root'
    ]
]
```

Add your database username and password in 'username' and 'password' field. In 'database_name' add name of orientdb database which you want to connect and use.

## Migration

To create a migration, you may use the orient command on the Artisan CLI:

```php
php artisan orient:make create_users_table
```

The migration will be placed in your database/migrations folder, and will contain a timestamp which allows the framework to determine the order of the migrations.

The --table and --create options may also be used to indicate the name of the table, and whether the migration will be creating a new table:
```php
php artisan orient:make add_votes_to_users_table --table=users_votes

php artisan orient:make create_users_table --create=users
```
To run migration 
```php
php artisan orient:migrate
```

## How to Use
```php
// To insert a record
class User extends \Orientdb {

    protected $fillable = ['name', 'email'];
}

$user = User::create(['name' => 'Some Name', 'email' => 'some@email.com']);

```
You can use this by extending Orientdb into model class. 


To fetch all records
```php
$users = User::all();
foreach($users as $user){
        echo $user->id;
        echo $user->name;
        echo $user->email;
    }
```
To find a record
```php
$user = User::find(1);
```
To update a record
```php
$user = User::find(1);
$user->name = "New Name";
$user->save();
```
## Relationships
To create one-to-one relationship
```php
$user =   User::create(['name'=>"Sumit", 'email' => "demo@email.com"]); // Create User node
$phone = new Phone(['code' => 963, 'number' => '98555533']); // Create Phone node
$relation = $user->has_phone()->save($phone); // Creating relationship
```
Unable to find has_phone() method ? [See full example.](https://github.com/sgpatil/orientdb-laravel-5/wiki/Relationships)


Want to learn more? [See the wiki.](https://github.com/sgpatil/orientdb-laravel-5/wiki)
