# Laravel Admin Panel Starter Kit with Tailwind CSS 4

A modern admin panel starter kit built with Laravel and Tailwind CSS 4, featuring modular Blade components and role-based access control.

## 📋 Available Versions

- **Laravel 10.x** - [View Laravel 10 Guide](#laravel-10x-version)
- **Laravel 11.x (Latest)** - [View Laravel 11 Guide](#laravel-11x-latest-version)

## ✨ Features

- ✅ Laravel with Blade components
- ✅ Tailwind CSS 4 (no config files required)
- ✅ FontAwesome icons
- ✅ Vite build system
- ✅ Responsive sidebar and navbar
- ✅ Flash notifications
- ✅ Role-based access control
- ✅ Dark mode support
- ✅ Modular component architecture

---

# Laravel 10.x Version

## Installation (Laravel 10)

### 1. Create Laravel 10 Project

```bash
composer create-project laravel/laravel admin-panel "10.*"
cd admin-panel
```

### 2. Install Compatible Laravel Breeze

```bash
# Install Breeze v1.x (compatible with Laravel 10)
composer require laravel/breeze:^1.19 --dev
php artisan breeze:install blade

# Remove Tailwind v3 installed by Breeze
npm uninstall tailwindcss postcss autoprefixer @tailwindcss/forms
```

### 3. Install Tailwind CSS 4 and Dependencies

```bash
# Remove Tailwind v3 config files if they exist
rm -f tailwind.config.js postcss.config.js

# Install Tailwind CSS 4 and FontAwesome
npm install @tailwindcss/vite @fortawesome/fontawesome-free
```

### 4. Clean Up Breeze's Tailwind v3 CSS

Replace the entire content of `resources/css/app.css` (remove Breeze's default imports):

### 5. Configure Vite

Update `vite.config.js` (replace Breeze's config):

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        tailwindcss(),
    ],
});
```

### 6. Configure Tailwind CSS 4

Update `resources/css/app.css`:

```css
/* File: resources/css/app.css (Struktur yang Benar untuk v4) */
/* Impor font atau file CSS lain yang valid tetap di sini */
@import "tailwindcss";
@import "@fortawesome/fontawesome-free/css/all.min.css";

@custom-variant dark (&:where(.dark, .dark *));

/* (Opsional) Memberitahu Tailwind di mana harus mencari kelas-kelas utility */
@source "resources/views/**/*.blade.php";

/* Arahan v4 untuk kustomisasi tema langsung di CSS */
@theme {
  --color-primary: #3b82f6;
  --color-primary-50: #eff6ff;
  --color-primary-100: #dbeafe;
  --color-primary-500: #3b82f6;
  --color-primary-600: #2563eb;
  --color-primary-700: #1d4ed8;
  --color-primary-900: #1e3a8a;
  
  --color-success: #10b981;
  --color-warning: #f59e0b;
  --color-error: #ef4444;
  --color-info: #3b82f6;
}

/* Layer kustom Anda tetap di sini */
@layer base {
  html {
    @apply h-full;
  }
  
  body {
    @apply h-full bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100;
  }
}

@layer components {
  .btn {
    @apply px-4 py-2 rounded-lg font-medium transition-colors duration-200;
  }
  
  .btn-primary {
    @apply bg-primary-500 text-white hover:bg-primary-600;
  }
  
  .btn-secondary {
    @apply bg-gray-200 text-gray-900 hover:bg-gray-300 dark:bg-gray-700 dark:text-gray-100 dark:hover:bg-gray-600;
  }
}
```

## Alternative Approach: Manual Authentication (Laravel 10)

If you prefer to avoid Breeze compatibility issues with Laravel 10, you can set up authentication manually:

### Option A: Laravel UI (Laravel 10)

```bash
# Install Laravel UI instead of Breeze
composer require laravel/ui
php artisan ui bootstrap --auth
# Or use Vue/React variant

# Then continue with Tailwind 4 setup
npm install @tailwindcss/vite @fortawesome/fontawesome-free
```

### Option B: Manual Authentication Setup (Laravel 10)

```bash
# Create authentication controllers manually
php artisan make:controller Auth/LoginController
php artisan make:controller Auth/RegisterController
php artisan make:controller Auth/LogoutController

# Create authentication views manually
mkdir -p resources/views/auth
```

Create login form (`resources/views/auth/login.blade.php`):
```php
<x-layouts.app title="Login">
    <div class="min-h-screen flex items-center justify-center bg-gray-50 dark:bg-gray-900 py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-md w-full space-y-8">
            <div>
                <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900 dark:text-white">
                    Sign in to your account
                </h2>
            </div>
            
            <form class="mt-8 space-y-6" method="POST" action="{{ route('login') }}">
                @csrf
                
                <div class="rounded-md shadow-sm -space-y-px">
                    <div>
                        <label for="email" class="sr-only">Email address</label>
                        <input id="email" name="email" type="email" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Email address" value="{{ old('email') }}">
                        @error('email')
                            <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
                        @enderror
                    </div>
                    
                    <div>
                        <label for="password" class="sr-only">Password</label>
                        <input id="password" name="password" type="password" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Password">
                        @error('password')
                            <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
                        @enderror
                    </div>
                </div>

                <div class="flex items-center justify-between">
                    <div class="flex items-center">
                        <input id="remember" name="remember" type="checkbox" 
                               class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                        <label for="remember" class="ml-2 block text-sm text-gray-900 dark:text-gray-300">
                            Remember me
                        </label>
                    </div>
                </div>

                <div>
                    <button type="submit" 
                            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-primary-600 hover:bg-primary-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500">
                        Sign in
                    </button>
                </div>
                
                <div class="text-center">
                    <a href="{{ route('register') }}" class="text-primary-600 hover:text-primary-500 dark:text-primary-400">
                        Don't have an account? Register here
                    </a>
                </div>
            </form>
        </div>
    </div>
</x-layouts.app>
```

Create register form (`resources/views/auth/register.blade.php`):
```php
<x-layouts.app title="Register">
    <div class="min-h-screen flex items-center justify-center bg-gray-50 dark:bg-gray-900 py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-md w-full space-y-8">
            <div>
                <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900 dark:text-white">
                    Create your account
                </h2>
            </div>
            
            <form class="mt-8 space-y-6" method="POST" action="{{ route('register') }}">
                @csrf
                
                <div class="rounded-md shadow-sm -space-y-px">
                    <div>
                        <label for="name" class="sr-only">Full name</label>
                        <input id="name" name="name" type="text" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Full name" value="{{ old('name') }}">
                        @error('name')
                            <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
                        @enderror
                    </div>
                    
                    <div>
                        <label for="email" class="sr-only">Email address</label>
                        <input id="email" name="email" type="email" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Email address" value="{{ old('email') }}">
                        @error('email')
                            <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
                        @enderror
                    </div>
                    
                    <div>
                        <label for="password" class="sr-only">Password</label>
                        <input id="password" name="password" type="password" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Password">
                        @error('password')
                            <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
                        @enderror
                    </div>
                    
                    <div>
                        <label for="password_confirmation" class="sr-only">Confirm Password</label>
                        <input id="password_confirmation" name="password_confirmation" type="password" required 
                               class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-primary-500 focus:border-primary-500 focus:z-10 sm:text-sm dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400" 
                               placeholder="Confirm Password">
                    </div>
                </div>

                <div>
                    <button type="submit" 
                            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-primary-600 hover:bg-primary-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500">
                        Create Account
                    </button>
                </div>
                
                <div class="text-center">
                    <a href="{{ route('login') }}" class="text-primary-600 hover:text-primary-500 dark:text-primary-400">
                        Already have an account? Sign in here
                    </a>
                </div>
            </form>
        </div>
    </div>
</x-layouts.app>
```

Create authentication routes (`routes/web.php`):
```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\Auth\LoginController;
use App\Http\Controllers\Auth\RegisterController;
use App\Http\Controllers\DashboardController;

Route::get('/', function () {
    return view('welcome');
});

// Authentication Routes
Route::middleware('guest')->group(function () {
    Route::get('/login', [LoginController::class, 'showLoginForm'])->name('login');
    Route::post('/login', [LoginController::class, 'login']);
    Route::get('/register', [RegisterController::class, 'showRegistrationForm'])->name('register');
    Route::post('/register', [RegisterController::class, 'register']);
});

Route::post('/logout', [LoginController::class, 'logout'])->name('logout')->middleware('auth');

// Admin routes
Route::middleware(['auth', 'verified', 'admin'])->prefix('admin')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index'])->name('dashboard');
});

Route::redirect('/dashboard', '/admin/dashboard');
```

Create Register Controller (`app/Http/Controllers/Auth/RegisterController.php`):
```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\Auth;

class RegisterController extends Controller
{
    public function showRegistrationForm()
    {
        return view('auth.register');
    }

    public function register(Request $request)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:8|confirmed',
        ]);

        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => Hash::make($request->password),
            'role' => 'user', // Default role
        ]);

        Auth::login($user);

        return redirect('/');
    }
}
```

## Step-by-Step Setup Commands

Run these commands in order to set up the directory structure:

```bash
# Create the component directories
mkdir -p resources/views/components/layouts
mkdir -p resources/views/pages
mkdir -p resources/views/auth

# Create the base layout component
touch resources/views/components/layouts/app.blade.php

# Create other components
touch resources/views/components/admin.blade.php
touch resources/views/components/alert.blade.php
touch resources/views/components/card.blade.php
touch resources/views/components/navbar.blade.php
touch resources/views/components/sidebar.blade.php

# Create pages
touch resources/views/pages/dashboard.blade.php

# Create auth views (if using manual authentication)
touch resources/views/auth/login.blade.php
touch resources/views/auth/register.blade.php

# Create auth controllers (if using manual authentication)
php artisan make:controller Auth/LoginController
php artisan make:controller Auth/RegisterController
```
```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class LoginController extends Controller
{
    public function showLoginForm()
    {
        return view('auth.login');
    }

    public function login(Request $request)
    {
        $credentials = $request->validate([
            'email' => 'required|email',
            'password' => 'required',
        ]);

        if (Auth::attempt($credentials, $request->boolean('remember'))) {
            $request->session()->regenerate();

            // Redirect to admin dashboard if user has admin role
            if (in_array(Auth::user()->role, ['admin', 'moderator'])) {
                return redirect()->intended('/admin/dashboard');
            }

            return redirect()->intended('/');
        }

        return back()->withErrors([
            'email' => 'The provided credentials do not match our records.',
        ])->onlyInput('email');
    }

    public function logout(Request $request)
    {
        Auth::logout();
        $request->session()->invalidate();
        $request->session()->regenerateToken();

        return redirect('/');
    }
}
```

## Recommended Approach (Laravel 10)

**For Laravel 10, I recommend Option B (Manual Authentication)** because:
1. ✅ No version conflicts
2. ✅ Full control over authentication flow  
3. ✅ Clean Tailwind 4 integration
4. ✅ No legacy Tailwind v3 remnants
5. ✅ Lighter weight (no unnecessary Breeze dependencies)

### Database Migration & Seeder

Add role column to users and create admin user:

```bash
php artisan make:migration add_role_to_users_table
```

```php
// database/migrations/xxxx_add_role_to_users_table.php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->string('role')->default('user')->after('email');
        });
    }

    public function down(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('role');
        });
    }
};
```

Create admin seeder:

```bash
php artisan make:seeder AdminUserSeeder
```

```php
// database/seeders/AdminUserSeeder.php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;
use App\Models\User;

class AdminUserSeeder extends Seeder
{
    public function run(): void
    {
        User::create([
            'name' => 'Admin User',
            'email' => 'admin@example.com',
            'password' => Hash::make('password'),
            'role' => 'admin',
            'email_verified_at' => now(),
        ]);

        User::create([
            'name' => 'Moderator User',
            'email' => 'moderator@example.com',
            'password' => Hash::make('password'),
            'role' => 'moderator',
            'email_verified_at' => now(),
        ]);
    }
}
```

Update `database/seeders/DatabaseSeeder.php`:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        $this->call([
            AdminUserSeeder::class,
        ]);
    }
}
```

### Gates Setup (Laravel 10)

Update `app/Providers/AuthServiceProvider.php`:

```php
<?php

namespace App\Providers;

use Illuminate\Foundation\Support\Providers\AuthServiceProvider as ServiceProvider;
use Illuminate\Support\Facades\Gate;

class AuthServiceProvider extends ServiceProvider
{
    protected $policies = [
        // 'App\Models\Model' => 'App\Policies\ModelPolicy',
    ];

    public function boot(): void
    {
        $this->registerPolicies();

        // Admin Gates
        Gate::define('view-dashboard', function ($user) {
            return in_array($user->role, ['admin', 'moderator']);
        });

        Gate::define('view-users', function ($user) {
            return $user->role === 'admin';
        });

        Gate::define('view-settings', function ($user) {
            return $user->role === 'admin';
        });
    }
}
```

### Admin Middleware (Laravel 10)

Create middleware:

```bash
php artisan make:middleware AdminMiddleware
```

```php
// app/Http/Middleware/AdminMiddleware.php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class AdminMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        if (!auth()->check()) {
            return redirect()->route('login');
        }

        if (!in_array(auth()->user()->role, ['admin', 'moderator'])) {
            abort(403, 'Access denied. Admin privileges required.');
        }

        return $next($request);
    }
}
```

Register middleware in `app/Http/Kernel.php`:

```php
<?php

namespace App\Http;

use Illuminate\Foundation\Http\Kernel as HttpKernel;

class Kernel extends HttpKernel
{
    // ... existing code ...

    protected $middlewareAliases = [
        // ... existing middleware ...
        'admin' => \App\Http\Middleware\AdminMiddleware::class,
    ];
}
```

## Routes (Laravel 10)

### Web Routes (`routes/web.php`)

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\DashboardController;

Route::get('/', function () {
    return view('welcome');
});

// Admin routes - protected by auth and admin middleware
Route::middleware(['auth', 'verified', 'admin'])->prefix('admin')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index'])
        ->name('dashboard');
});

// Redirect /dashboard to /admin/dashboard for convenience
Route::redirect('/dashboard', '/admin/dashboard');

require __DIR__.'/auth.php';
```

---

# Laravel 11.x (Latest) Version

## Installation (Laravel 11)

### 1. Create Laravel 11 Project

```bash
composer create-project laravel/laravel admin-panel
cd admin-panel
```

### 2. Install Laravel Breeze (Authentication)

```bash
# Laravel 11 uses Breeze v2.x which has better Tailwind 4 compatibility
composer require laravel/breeze --dev
php artisan breeze:install blade

# Remove default Tailwind v3 dependencies if installed
npm uninstall tailwindcss postcss autoprefixer @tailwindcss/forms
```

### 3. Install Tailwind CSS 4 and Dependencies

```bash
npm install @tailwindcss/vite @fortawesome/fontawesome-free

# Remove config files if they exist
rm -f tailwind.config.js postcss.config.js
```

### 4. Configure Vite (same as Laravel 10)

Update `vite.config.js`:

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        tailwindcss(),
    ],
});
```

### 5. Configure Tailwind CSS 4 (same as Laravel 10)

Update `resources/css/app.css` - use the same configuration as Laravel 10 version above.

## Authentication & Authorization (Laravel 11)

### Database Migration & Seeder (same as Laravel 10)

Use the same migration and seeder files as Laravel 10 version above.

### Gates Setup (Laravel 11)

Update `app/Providers/AppServiceProvider.php` (Laravel 11 doesn't have separate AuthServiceProvider by default):

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Gate;

class AppServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        //
    }

    public function boot(): void
    {
        // Admin Gates
        Gate::define('view-dashboard', function ($user) {
            return in_array($user->role, ['admin', 'moderator']);
        });

        Gate::define('view-users', function ($user) {
            return $user->role === 'admin';
        });

        Gate::define('view-settings', function ($user) {
            return $user->role === 'admin';
        });
    }
}
```

### Admin Middleware (Laravel 11)

Create middleware:

```bash
php artisan make:middleware AdminMiddleware
```

```php
// app/Http/Middleware/AdminMiddleware.php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class AdminMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        if (!auth()->check()) {
            return redirect()->route('login');
        }

        if (!in_array(auth()->user()->role, ['admin', 'moderator'])) {
            abort(403, 'Access denied. Admin privileges required.');
        }

        return $next($request);
    }
}
```

Register middleware in `bootstrap/app.php`:

```php
<?php

use Illuminate\Foundation\Application;
use Illuminate\Foundation\Configuration\Exceptions;
use Illuminate\Foundation\Configuration\Middleware;

return Application::configure(basePath: dirname(__DIR__))
    ->withRouting(
        web: __DIR__.'/../routes/web.php',
        commands: __DIR__.'/../routes/console.php',
        health: '/up',
    )
    ->withMiddleware(function (Middleware $middleware) {
        $middleware->alias([
            'admin' => \App\Http\Middleware\AdminMiddleware::class,
        ]);
    })
    ->withExceptions(function (Exceptions $exceptions) {
        //
    })->create();
```

## Routes (Laravel 11 - same as Laravel 10)

Use the same routes configuration as Laravel 10 version above.

---

# Shared Components (Both Versions)

## Directory Structure

Create the following directory structure:

```
resources/views/
├── components/
│   ├── layouts/
│   │   └── app.blade.php
│   ├── admin.blade.php
│   ├── alert.blade.php
│   ├── card.blade.php
│   ├── navbar.blade.php
│   └── sidebar.blade.php
└── pages/
    └── dashboard.blade.php
```

**Important:** The `app.blade.php` layout should be inside `resources/views/components/layouts/` directory, NOT `resources/views/layouts/`.

## Blade Components

### Base Layout (`resources/views/components/layouts/app.blade.php`)

**Create this file in the correct path: `resources/views/components/layouts/app.blade.php`**

```php
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}" class="{{ request()->cookie('theme', 'light') }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="csrf-token" content="{{ csrf_token() }}">
    
    <title>{{ $title ?? config('app.name') }}</title>
    
    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
<body>
    {{ $slot }}
    
    <script>
        // Dark mode toggle
        function toggleDarkMode() {
            const html = document.documentElement;
            const isDark = html.classList.contains('dark');
            
            if (isDark) {
                html.classList.remove('dark');
                document.cookie = 'theme=light; path=/; max-age=31536000';
            } else {
                html.classList.add('dark');
                document.cookie = 'theme=dark; path=/; max-age=31536000';
            }
        }
    </script>
</body>
</html>
```

### Admin Layout (`resources/views/components/admin.blade.php`)

```php
<x-layouts.app :title="$title ?? 'Admin Panel'">
    <div class="min-h-screen bg-gray-50 dark:bg-gray-900">
        <x-sidebar />
        
        <div class="lg:pl-64">
            <x-navbar />
            
            <main class="py-6">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <!-- Flash Messages -->
                    @if(session('success'))
                        <x-alert type="success" :message="session('success')" class="mb-6" />
                    @endif
                    
                    @if(session('error'))
                        <x-alert type="error" :message="session('error')" class="mb-6" />
                    @endif
                    
                    @if(session('warning'))
                        <x-alert type="warning" :message="session('warning')" class="mb-6" />
                    @endif
                    
                    @if(session('info'))
                        <x-alert type="info" :message="session('info')" class="mb-6" />
                    @endif
                    
                    <!-- Page Content -->
                    {{ $slot }}
                </div>
            </main>
        </div>
    </div>
</x-layouts.app>
```

### Sidebar (`resources/views/components/sidebar.blade.php`)

```php
@props(['class' => ''])

<div class="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-64 lg:flex-col {{ $class }}">
    <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-white dark:bg-gray-800 px-6 border-r border-gray-200 dark:border-gray-700">
        <div class="flex h-16 shrink-0 items-center">
            <h1 class="text-xl font-bold text-gray-900 dark:text-white">Admin Panel</h1>
        </div>
        
        <nav class="flex flex-1 flex-col">
            <ul role="list" class="flex flex-1 flex-col gap-y-7">
                <li>
                    <ul role="list" class="-mx-2 space-y-1">
                        @can('view-dashboard')
                        <li>
                            <a href="{{ route('dashboard') }}" 
                               class="group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold {{ request()->routeIs('dashboard') ? 'bg-primary-50 text-primary-600 dark:bg-primary-900/50 dark:text-primary-400' : 'text-gray-700 hover:text-primary-600 hover:bg-gray-50 dark:text-gray-300 dark:hover:text-white dark:hover:bg-gray-700' }}">
                                <i class="fas fa-home w-5 h-5 shrink-0"></i>
                                Dashboard
                            </a>
                        </li>
                        @endcan
                        
                        @can('view-users')
                        <li>
                            <a href="#" 
                               class="group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold text-gray-700 hover:text-primary-600 hover:bg-gray-50 dark:text-gray-300 dark:hover:text-white dark:hover:bg-gray-700">
                                <i class="fas fa-users w-5 h-5 shrink-0"></i>
                                Users
                            </a>
                        </li>
                        @endcan
                        
                        @can('view-settings')
                        <li>
                            <a href="#" 
                               class="group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold text-gray-700 hover:text-primary-600 hover:bg-gray-50 dark:text-gray-300 dark:hover:text-white dark:hover:bg-gray-700">
                                <i class="fas fa-cog w-5 h-5 shrink-0"></i>
                                Settings
                            </a>
                        </li>
                        @endcan
                    </ul>
                </li>
            </ul>
        </nav>
    </div>
</div>

<!-- Mobile sidebar -->
<div class="lg:hidden">
    <div class="fixed inset-0 z-50 hidden" id="mobile-sidebar">
        <div class="fixed inset-0 bg-gray-900/80" onclick="toggleMobileSidebar()"></div>
        <div class="fixed inset-y-0 left-0 z-50 w-64 bg-white dark:bg-gray-800 px-6 border-r border-gray-200 dark:border-gray-700">
            <div class="flex h-16 shrink-0 items-center justify-between">
                <h1 class="text-xl font-bold text-gray-900 dark:text-white">Admin Panel</h1>
                <button onclick="toggleMobileSidebar()" class="text-gray-500 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-200">
                    <i class="fas fa-times w-5 h-5"></i>
                </button>
            </div>
            <!-- Same navigation as desktop -->
        </div>
    </div>
</div>

<script>
function toggleMobileSidebar() {
    const sidebar = document.getElementById('mobile-sidebar');
    sidebar.classList.toggle('hidden');
}
</script>
```

### Navbar (`resources/views/components/navbar.blade.php`)

```php
<header class="sticky top-0 z-40 bg-white dark:bg-gray-800 shadow-sm border-b border-gray-200 dark:border-gray-700">
    <div class="px-4 sm:px-6 lg:px-8">
        <div class="flex h-16 justify-between items-center">
            <div class="flex items-center">
                <button onclick="toggleMobileSidebar()" class="lg:hidden text-gray-500 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-200">
                    <i class="fas fa-bars w-5 h-5"></i>
                </button>
            </div>
            
            <div class="flex items-center gap-x-4">
                <!-- Dark mode toggle -->
                <button onclick="toggleDarkMode()" class="text-gray-500 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-200">
                    <i class="fas fa-moon w-5 h-5 dark:hidden"></i>
                    <i class="fas fa-sun w-5 h-5 hidden dark:block"></i>
                </button>
                
                <!-- User dropdown -->
                <div class="relative">
                    <button class="flex items-center text-sm rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500">
                        <img class="h-8 w-8 rounded-full" src="https://ui-avatars.com/api/?name={{ urlencode(auth()->user()->name ?? 'User') }}&background=3b82f6&color=fff" alt="User avatar">
                        <span class="ml-2 text-gray-700 dark:text-gray-300">{{ auth()->user()->name ?? 'User' }}</span>
                        <i class="fas fa-chevron-down w-4 h-4 ml-1 text-gray-500"></i>
                    </button>
                    
                    <!-- Dropdown menu (you can implement with Alpine.js or vanilla JS) -->
                    <div class="hidden absolute right-0 mt-2 w-48 bg-white dark:bg-gray-800 rounded-md shadow-lg border border-gray-200 dark:border-gray-700">
                        <a href="#" class="block px-4 py-2 text-sm text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-700">Profile</a>
                        <form method="POST" action="{{ route('logout') }}">
                            @csrf
                            <button type="submit" class="block w-full text-left px-4 py-2 text-sm text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-700">
                                Logout
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</header>
```

### Alert Component (`resources/views/components/alert.blade.php`)

```php
@props([
    'type' => 'info',
    'message' => '',
    'dismissible' => true
])

@php
$classes = [
    'success' => 'bg-green-50 border-green-200 text-green-800 dark:bg-green-900/50 dark:border-green-800 dark:text-green-200',
    'error' => 'bg-red-50 border-red-200 text-red-800 dark:bg-red-900/50 dark:border-red-800 dark:text-red-200',
    'warning' => 'bg-yellow-50 border-yellow-200 text-yellow-800 dark:bg-yellow-900/50 dark:border-yellow-800 dark:text-yellow-200',
    'info' => 'bg-blue-50 border-blue-200 text-blue-800 dark:bg-blue-900/50 dark:border-blue-800 dark:text-blue-200',
];

$icons = [
    'success' => 'fas fa-check-circle',
    'error' => 'fas fa-exclamation-circle',
    'warning' => 'fas fa-exclamation-triangle',
    'info' => 'fas fa-info-circle',
];
@endphp

<div {{ $attributes->merge(['class' => 'border rounded-lg p-4 ' . $classes[$type]]) }} 
     @if($dismissible) x-data="{ show: true }" x-show="show" @endif>
    <div class="flex items-start">
        <div class="flex-shrink-0">
            <i class="{{ $icons[$type] }} w-5 h-5"></i>
        </div>
        <div class="ml-3 flex-1">
            <p class="text-sm font-medium">{{ $message }}</p>
            @if($slot->isNotEmpty())
                <div class="mt-2 text-sm">
                    {{ $slot }}
                </div>
            @endif
        </div>
        @if($dismissible)
        <div class="ml-auto pl-3">
            <button @click="show = false" class="inline-flex rounded-md p-1.5 focus:outline-none focus:ring-2 focus:ring-offset-2">
                <i class="fas fa-times w-4 h-4"></i>
            </button>
        </div>
        @endif
    </div>
</div>
```

### Card Component (`resources/views/components/card.blade.php`)

```php
@props([
    'title' => '',
    'subtitle' => '',
    'padding' => 'p-6'
])

<div {{ $attributes->merge(['class' => 'bg-white dark:bg-gray-800 shadow rounded-lg border border-gray-200 dark:border-gray-700']) }}>
    @if($title || $subtitle)
    <div class="px-6 py-4 border-b border-gray-200 dark:border-gray-700">
        @if($title)
        <h3 class="text-lg font-medium text-gray-900 dark:text-white">{{ $title }}</h3>
        @endif
        @if($subtitle)
        <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">{{ $subtitle }}</p>
        @endif
    </div>
    @endif
    
    <div class="{{ $padding }}">
        {{ $slot }}
    </div>
</div>
```

## Dashboard Controller (Both Versions)

### Dashboard Controller (`app/Http/Controllers/DashboardController.php`)

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class DashboardController extends Controller
{
    public function index()
    {
        return view('pages.dashboard');
    }
}
```

## Dashboard Page Example

### Dashboard View (`resources/views/pages/dashboard.blade.php`)

```php
<x-admin title="Dashboard">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
        <!-- Stats Cards -->
        <x-card class="text-center">
            <div class="text-3xl font-bold text-primary-600 dark:text-primary-400">150</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Total Users</div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-green-600 dark:text-green-400">89</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Active Sessions</div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-yellow-600 dark:text-yellow-400">12</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Pending</div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-red-600 dark:text-red-400">3</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Issues</div>
        </x-card>
    </div>
    
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Recent Activity -->
        <x-card title="Recent Activity" subtitle="Latest system activities">
            <div class="space-y-4">
                <div class="flex items-center space-x-3">
                    <div class="flex-shrink-0">
                        <i class="fas fa-user-plus text-green-500"></i>
                    </div>
                    <div class="flex-1">
                        <p class="text-sm text-gray-900 dark:text-white">New user registered</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">2 minutes ago</p>
                    </div>
                </div>
                
                <div class="flex items-center space-x-3">
                    <div class="flex-shrink-0">
                        <i class="fas fa-edit text-blue-500"></i>
                    </div>
                    <div class="flex-1">
                        <p class="text-sm text-gray-900 dark:text-white">Settings updated</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">1 hour ago</p>
                    </div>
                </div>
                
                <div class="flex items-center space-x-3">
                    <div class="flex-shrink-0">
                        <i class="fas fa-trash text-red-500"></i>
                    </div>
                    <div class="flex-1">
                        <p class="text-sm text-gray-900 dark:text-white">User account deleted</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">3 hours ago</p>
                    </div>
                </div>
            </div>
        </x-card>
        
        <!-- Quick Actions -->
        <x-card title="Quick Actions" subtitle="Commonly used admin actions">
            <div class="grid grid-cols-2 gap-4">
                <button class="btn btn-primary flex items-center justify-center space-x-2">
                    <i class="fas fa-user-plus"></i>
                    <span>Add User</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2">
                    <i class="fas fa-cog"></i>
                    <span>Settings</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2">
                    <i class="fas fa-chart-bar"></i>
                    <span>Reports</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2">
                    <i class="fas fa-download"></i>
                    <span>Export</span>
                </button>
            </div>
        </x-card>
    </div>
</x-admin>
```

## Build and Run (Both Versions)

```bash
# Install dependencies
npm install

# Build assets for development
npm run dev

# Or build for production
npm run build

# Run migrations and seed admin users
php artisan migrate
php artisan db:seed

# Run Laravel development server
php artisan serve
```

## Default Login Credentials

After running the seeders, you can login with:

**Admin User:**
- Email: `admin@example.com`
- Password: `password`
- Role: `admin` (full access)

**Moderator User:**
- Email: `moderator@example.com`
- Password: `password`
- Role: `moderator` (limited access)

## Access URLs

- **Login:** `http://localhost:8000/login`
- **Register:** `http://localhost:8000/register`
- **Admin Dashboard:** `http://localhost:8000/admin/dashboard`
- **Logout:** Available from the navbar dropdown

## Usage Examples

### Creating Flash Messages in Controllers

```php
// Success message
return redirect()->route('dashboard')->with('success', 'Operation completed successfully!');

// Error message  
return redirect()->back()->with('error', 'Something went wrong!');

// Warning message
return redirect()->back()->with('warning', 'Please check your input!');

// Info message
return redirect()->back()->with('info', 'Here is some information.');
```

### Custom Page with Admin Layout

```php
<x-admin title="Users Management">
    <div class="flex justify-between items-center mb-6">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white">Users</h1>
        <button class="btn btn-primary">
            <i class="fas fa-plus mr-2"></i>
            Add User
        </button>
    </div>
    
    <x-card>
        <!-- Your content here -->
        <p>Users table and management interface...</p>
    </x-card>
</x-admin>
```

### Adding New Admin Routes

For Laravel 10, add to `routes/web.php`:
```php
Route::middleware(['auth', 'verified', 'admin'])->prefix('admin')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index'])->name('dashboard');
    Route::get('/users', [UserController::class, 'index'])->name('admin.users');
    Route::get('/settings', [SettingController::class, 'index'])->name('admin.settings');
});
```

For Laravel 11, use the same route structure.

### Creating New Components

```bash
# Create a new component
php artisan make:component Button

# Create a component in a subdirectory
php artisan make:component Forms/Input
```

Example button component (`resources/views/components/button.blade.php`):
```php
@props([
    'type' => 'button',
    'variant' => 'primary',
    'size' => 'md'
])

@php
$classes = [
    'primary' => 'btn btn-primary',
    'secondary' => 'btn btn-secondary',
];

$sizes = [
    'sm' => 'px-3 py-1.5 text-sm',
    'md' => 'px-4 py-2',
    'lg' => 'px-6 py-3 text-lg',
];
@endphp

<button 
    type="{{ $type }}"
    {{ $attributes->merge(['class' => $classes[$variant] . ' ' . $sizes[$size]]) }}
>
    {{ $slot }}
</button>
```

Usage:
```php
<x-button variant="primary" size="lg">Save Changes</x-button>
```

## Key Differences Between Laravel 10 & 11

| Feature | Laravel 10 | Laravel 11 |
|---------|------------|------------|
| **Middleware Registration** | `app/Http/Kernel.php` | `bootstrap/app.php` |
| **Gates/Policies** | `AuthServiceProvider.php` | `AppServiceProvider.php` |
| **Directory Structure** | Traditional structure | Simplified structure |
| **Service Providers** | Separate Auth provider | Consolidated in App provider |
| **Configuration** | More config files | Streamlined config |

## Troubleshooting

### Common Issues

**1. Laravel 10 + Breeze Version Conflicts:**
```bash
# Error: laravel/breeze requires illuminate/console ^11.0
# Solution: Use compatible version
composer require laravel/breeze:^1.19 --dev

# Or use manual authentication approach (recommended)
```

**2. Tailwind v3 vs v4 Conflicts:**
```bash
# Remove Tailwind v3 dependencies
npm uninstall tailwindcss postcss autoprefixer @tailwindcss/forms

# Remove config files
rm -f tailwind.config.js postcss.config.js

# Install Tailwind v4
npm install @tailwindcss/vite

# Clear cache
npm run build --clean
```

**3. Breeze views still using Tailwind v3 classes:**
- Manually update Breeze generated views to use Tailwind v4 compatible classes
- Or use manual authentication approach to avoid this issue

**4. Component path error (Unable to locate component [layouts.app]):**
```bash
# Ensure the file is in the correct location:
# resources/views/components/layouts/app.blade.php (NOT layouts/app.blade.php)

# Check if the component directory structure is correct:
ls -la resources/views/components/layouts/

# Clear view cache
php artisan view:clear
```

**5. Tailwind styles not loading:**
```bash
# Clear cache and rebuild
npm run build
php artisan view:clear
php artisan config:clear
```

**2. FontAwesome icons not showing:**
- Ensure `@import "@fortawesome/fontawesome-free/css/all.min.css";` is in `app.css`
- Run `npm install` and `npm run build`

**3. Admin middleware not working:**
- Check middleware registration in correct file (Kernel.php vs bootstrap/app.php)
- Verify user has correct role in database

**4. Gates not working:**
- Ensure gates are defined in correct provider (AuthServiceProvider vs AppServiceProvider)
- Check user is authenticated before testing gates

**5. Dark mode toggle not working:**
- Ensure JavaScript function is loaded
- Check cookie theme value is being set correctly

### Performance Tips

1. **Production builds:**
   ```bash
   npm run build
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   ```

2. **Optimize images:**
   - Use optimized avatar images instead of UI Avatars API in production
   - Implement lazy loading for dashboard cards

3. **Database optimization:**
   - Add indexes to frequently queried columns (role, email)
   - Use database seeders for test data

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Changelog

### v1.2.0
- Added support for Laravel 11
- Updated middleware registration for Laravel 11
- Consolidated authentication setup

### v1.1.0
- Added dark mode support
- Improved responsive design
- Added flash notification system

### v1.0.0
- Initial release with Laravel 10 support
- Basic admin panel with Tailwind CSS 4
- Role-based access control

## License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Support

- **Documentation:** This README
- **Issues:** [GitHub Issues](https://github.com/your-username/laravel-admin-tailwind4/issues)
- **Discussions:** [GitHub Discussions](https://github.com/your-username/laravel-admin-tailwind4/discussions)

## Credits

- [Laravel](https://laravel.com) - The PHP Framework
- [Tailwind CSS](https://tailwindcss.com) - CSS Framework
- [FontAwesome](https://fontawesome.com) - Icon Library
- [Laravel Breeze](https://laravel.com/docs/starter-kits#laravel-breeze) - Authentication Scaffolding
