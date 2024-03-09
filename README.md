## Permission-and-Role-Base-User-Management-System Using Laravel

## Purpose of this project 

<p> 1) Implement Role and Permission Based Authentication and Authorizom System</p>
<p> 2) Dynamically Crate Role and Assign to the User</p>
<p> 3) Authrizom can be provide Based on Role </p>
<p> 4) Role can be create based on Route </p>
<p> 5) Update Role and Have CRUD Functionality</p>
..happy coding

## Laravel 8 User Roles and Permissions Tutorial

### Step 1: composer create-project --prefer-dist laravel/laravel blog
```
composer create-project --prefer-dist laravel/laravel user_role
```

### Step 2: Install Composer Packages
```
composer require spatie/laravel-permission
```
```
composer require laravelcollective/html
```

### Now open config/app.php file and add service provider and aliase. 
``` config/app.php
'providers' => [

	....

	Spatie\Permission\PermissionServiceProvider::class,

],
```
We can also custom changes on Spatie package, so if you also want to changes then you can fire bellow command and get config file in config/permission.php and migration files.

```
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
```

Now you can see permission.php file and one migrations. so you can run migration using following command:

```
php artisan migrate
```

### Step 3: Create Models

In this step we have to create model for User and Product table, so if you get fresh project then you have User Model have so just replace code and other you should create.

```app/Models/User.php
<?php
  
namespace App\Models;
  
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Spatie\Permission\Traits\HasRoles;
  
class User extends Authenticatable
{
    use HasFactory, Notifiable, HasRoles;
  
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'name',
        'email',
        'password',
    ];
  
    /**
     * The attributes that should be hidden for arrays.
     *
     * @var array
     */
    protected $hidden = [
        'password',
        'remember_token',
    ];
  
    /**
     * The attributes that should be cast to native types.
     *
     * @var array
     */
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];
}
```

### Step 4: Add Middleware
Spatie package provide it's in-built middleware that way we can use it simply and that is display as bellow:

role
permission

So, we have to add middleware in Kernel.php file this way :

```app/Http/Kernel.php
....
protected $routeMiddleware = [
    ....
    'role' => \Spatie\Permission\Middlewares\RoleMiddleware::class,
    'permission' => \Spatie\Permission\Middlewares\PermissionMiddleware::class,
    'role_or_permission' => \Spatie\Permission\Middlewares\RoleOrPermissionMiddleware::class,
]
....
```

### Step 5: Create Authentication
You have to follow few step to make auth in your laravel 8 application.

First you need to install laravel/ui package as like bellow:
```
composer require laravel/ui
```

Here, we need to generate auth scaffolding in laravel 8 using laravel ui command. so, let's generate it by bellow command:

```
php artisan ui bootstrap --auth
```



