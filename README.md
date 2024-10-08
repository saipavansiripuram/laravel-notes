# Laravel-Notes

# Laravel Project Setup

## Installation

To install Laravel, use Composer:

```bash
composer create-project laravel/laravel project-name
```

This command installs the necessary dependencies and files needed to run a Laravel project.

## Running the Built-in Webserver

After installation, you can start the Laravel development server:

```bash
php artisan serve
```

This command will run your application on `http://localhost:8000`.

## MVC Structure in Laravel

### Controllers (C in MVC)
Controllers are classes that group related logic and respond to route requests. Instead of manually creating controllers, you can generate one with Artisan:

```bash
php artisan make:controller UserController
```

You can assign routes to controller methods:

```php
Route::get('/users', [UserController::class, 'index']);
```

### Views (V in MVC)
The view layer is responsible for presenting the HTML content that is returned to the browser. Laravel uses Blade, a templating engine, to manage views.

To create a new view:

```bash
php artisan make:view file-name
```

You can also use a `view()` helper to return a view from a route:

```php
Route::get('/', function () {
    return view('welcome');
});
```

### Models (M in MVC)
Models are used to interact with the database and typically represent a table in your database. To generate a model with a migration:

```bash
php artisan make:model Product --migration
```

### Blade Templates
Blade is Laravel's templating engine that allows you to write clean and reusable views. It offers syntax enhancements like loops, conditionals, and template inheritance.

Example of Blade syntax:

```blade
<a href="{{ route('products.index') }}">Products</a>
```

You can also create layout templates using Blade's template inheritance feature:

```blade
// layout.blade.php
<html>
<head>
    <title>App Name - @yield('title')</title>
</head>
<body>
    @yield('content')
</body>
</html>

// home.blade.php
@extends('layout')

@section('title', 'Home')

@section('content')
    <h1>Welcome to our application</h1>
@endsection
```

To create a Blade component:

```bash
php artisan make:component Layout --view
```

## Facades

Facades in Laravel are used to provide a static interface to classes available in the service container. For example, the `Route` facade is commonly used to define routes in the `routes/web.php` file:

```php
Route::get('/', function () {
    return view('welcome');
});

Route::post('/submit', [FormController::class, 'submit']);
```

## Routing

Laravel provides a robust routing system. Routes can be defined in the `routes/web.php` file. Common route methods include:

```php
Route::get('/home', [HomeController::class, 'index']);
Route::post('/submit', [FormController::class, 'submit']);
Route::put('/update/{id}', [UpdateController::class, 'update']);
Route::delete('/delete/{id}', [DeleteController::class, 'destroy']);
```

Named routes allow you to refer to routes by name instead of URL:

```php
Route::get('/products', [ProductController::class, 'index'])->name('products.index');
```

Using a named route in Blade:

```blade
<a href="{{ route('products.index') }}">Products</a>
```

## Artisan

Laravel's Artisan command-line interface is a powerful tool for automating tasks. Some useful Artisan commands include:

```bash
php artisan list       # Lists all Artisan commands
php artisan make:controller ControllerName   # Creates a controller
php artisan migrate    # Runs database migrations
```

## Database Migrations

Migrations allow you to define the structure of your database. To create a migration:

```bash
php artisan make:migration create_products_table
```

After defining the schema in the migration file, you can run it:

```bash
php artisan migrate
```

## Eloquent ORM

Eloquent is Laravel's built-in ORM, allowing for easy database interaction. Example of an Eloquent model:

```php
class Product extends Model
{
    protected $fillable = ['name', 'price', 'description'];
}
```

You can perform CRUD operations using Eloquent:

```php
// Fetch all products
$products = Product::all();

// Create a new product
Product::create([
    'name' => 'Product Name',
    'price' => 100,
    'description' => 'Product Description',
]);

// Update a product
$product = Product::find(1);
$product->update(['price' => 200]);

// Delete a product
$product->delete();
```

## Validation

Laravel provides robust validation features. To validate a request in a controller method:

```php
public function store(Request $request)
{
    $request->validate([
        'name' => 'required|string|max:255',
        'price' => 'required|numeric',
    ]);

    // Store the data
}
```

## Route Model Binding

You can bind route parameters to Eloquent models automatically:

```php
Route::get('/products/{product}', function (Product $product) {
    return view('product.show', compact('product'));
});
```

## Pagination

Laravel provides a convenient way to paginate query results:

```php
$products = Product::paginate(10);
```

In Blade:

```blade
{{ $products->links() }}
```

## Flash Messages

Flash messages allow you to store a message in the session that will be available for the next request:

```php
session()->flash('status', 'Task was successful!');
```

In Blade:

```blade
@if (session('status'))
    <div class="alert alert-success">
        {{ session('status') }}
    </div>
@endif
```

## Updating Dependencies

To update all dependencies in your Laravel project, use the following command:

```bash
composer require laravel/framework "^8.0" --update-with-all-dependencies
```

## Helpful Links

- Laravel Documentation: [https://laravel.com/docs](https://laravel.com/docs)

---

This README should now provide a comprehensive guide for understanding the basics of Laravel, along with examples for installation, routing, Blade templates, controllers, and other key topics.
