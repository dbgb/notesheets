# PHP Development with Laravel <!-- omit in toc -->

- [Install steps](#install-steps)
- [Useful information & operations](#useful-information--operations)
  - [Project directories & structure](#project-directories--structure)
  - [Start a new project](#start-a-new-project)
  - [Manually refresh the application key](#manually-refresh-the-application-key)
  - [Generate login / registration scaffolding](#generate-login--registration-scaffolding)
  - [Set up a development database](#set-up-a-development-database)
  - [Migrate changes after modifying models / controllers](#migrate-changes-after-modifying-models--controllers)
  - [General project file generation](#general-project-file-generation)
  - [Monitor and compile development assets](#monitor-and-compile-development-assets)
  - [Interact with application data](#interact-with-application-data)
  - [Make local development assets available to the build environment](#make-local-development-assets-available-to-the-build-environment)
  - [Make application policies](#make-application-policies)
  - [Send emails via mailables](#send-emails-via-mailables)
  - [Use a debugging assistant](#use-a-debugging-assistant)
  - [Dump and die debugging](#dump-and-die-debugging)

---

## Install steps

1. Install Composer and add install location to path

   - eg. `C:\Users\<USER_NAME>\AppData\Roaming\Composer\vendor\bin`

2. Install Node.js and add install location to path

   - eg. `C:\Users\<USER_NAME>\AppData\Roaming\npm`

3. Install Laravel globally

   - `composer global require laravel/installer`

---

## Useful information & operations

### Project directories & structure

- refer to <https://laravel.com/docs/structure>

### Start a new project

```shell
laravel new <PROJECT_NAME> && cd $_
# OR composer create-project laravel/laravel <PROJECT_NAME> <VERSION>
php artisan serve
```

### Manually refresh the application key

```shell
php artisan key:generate
```

### Generate login / registration scaffolding

```shell
composer require laravel/ui
php artisan ui <UI_TYPE> --auth
npm install && npm run dev
```

### Set up a development database

```shell
# DB config is located at "config/database.php"
touch database/database.sqlite

# Edit ".env":
#   DB_CONNECTION=sqlite
#   delete other DB_ prefixed vars

php artisan migrate

```

### Migrate changes after modifying models / controllers

```shell
php artisan migrate
# OR to drop all tables and start fresh
php artisan migrate:fresh

php artisan migrate:status

# If required, rolls back the last migration
php artisan migrate:rollback

# If required, rolls back ALL migrations
php artisan migrate:reset
```

### General project file generation

```shell
# Make new validation rules, middleware etc.
php artisan make:<TYPE> <ARGS?>

# https://laravel.com/docs/5.1/controllers#restful-resource-controllers
php artisan make:controller --resource <NAME>

# Create new Eloquent model class, along with a migration file
php artisan make:model --migration <NAME>

# Then...
#   describe schema (fields, foreign keys, indexes etc.) in migration file
#   perform db migration
#   define any relationships in model classes
#   register routes for relevant HTTP verbs
#   create / modify views, as required
#   etc.

# Create pivot table for many:many relationship between two existing Models
# eg. for Profile and User models
# NB. naming conventions matter here
php artisan make:migration create_profile_user_pivot_table --create profile_user

# Then...
#   add the foreign keys to the pivot table (ie. profile_id, user_id)
#   perform db migration
```

### Monitor and compile development assets

```shell
npm run watch
```

### Interact with application data

```shell
php artisan tinker
```

```php
// Example: viewing and modifying user/profile information
$profile = new \App\Profile();
$profile->user_id = 1;
$profile->title = "Test title";
$profile->description = "Test description";
$profile->save();

$profile
>>> => App\Profile {#3208
>>>      title: "Test title",
>>>      description: "Test description",
>>>      user_id: 1,
>>>      updated_at: "2020-09-24 18:04:53",
>>>      created_at: "2020-09-24 18:04:53",
>>>      id: 1,
>>>      user: App\User {#4147
>>>        id: "1",
>>>        username: "dbgb",
>>>        email: "dbgb@mail.test",
>>>        email_verified_at: null,
>>>        created_at: "2020-09-23 11:04:34",
>>>        updated_at: "2020-09-23 11:04:34",
>>>      },
>>>    }

Profile::all();
$profile->user;

$user = User::find(1);
$user->profile;
$user->profile->url = "dbgb.dev";
$user->push();

// View an associated data object (NB: `posts` not invoked)
User::find(1)->posts->where("id", 4)

// Delete an associated data object (NB: `posts` is invoked)
User::find(1)->posts()->where("id", 4)->delete();
User::find(1)->posts()->where("id", ">=", "16")->delete();

// Drop all profiles
Profile::truncate();

// etc.
```

### Make local development assets available to the build environment

```shell
# Create a symbolic link from "public/storage" to "storage/app/public"
php artisan storage:link
```

### Make application policies

```shell
php artisan make:policy <POLICY_NAME> --model <MODEL_NAME>
```

### Send emails via mailables

```shell
php artisan make:mail <NAME> --markdown <TEMPLATE_VIEW_NAME>
# Then...
#   add mailer credentials to .env file
#   modify the email template in the views directory as desired
#   trigger mail on specific events
```

```php
# eg. on new user registration
# ...
 protected static function boot()
  {
    parent::boot();

    static::created(function ($user) {
      $user->profile()->create([
        "title" => $user->username,
      ]);
    });

    Mail::to($user->email)->send(new NewUserWelcomeMail());
  }
# ...
```

### Use a debugging assistant

```shell
# https://laravel.com/docs/5.8/telescope#introduction
composer require laravel/telescope --dev <VERSION>
php artisan telescope:install
php artisan migrate
# Visit <PROJECT_URL>/telescope
```

### Dump and die debugging

```php
// eg. inside a controller class
...
  public function show($user)
  {
    // display all user data matching the given user var
    dd(User::find($user));
  }
...
```
