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

## 🔧 System Requirements

- **PHP:** 8.1+ (Laravel 10) / 8.2+ (Laravel 11)  
- **Node.js:** 18+
- **Composer:** 2.0+
- **Database:** MySQL 5.7+ / PostgreSQL 10+ / SQLite 3.8+

## 🚀 Quick Start

### For Laravel 11 (Recommended)
```bash
# Clone or download the template
git clone https://github.com/your-username/laravel-admin-tailwind4.git admin-panel
cd admin-panel

# Install dependencies
composer install
npm install

# Setup environment
cp .env.example .env
php artisan key:generate

# Configure database in .env file
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=admin_panel
DB_USERNAME=root
DB_PASSWORD=

# Run migrations and seed data
php artisan migrate --seed

# Build assets and start server
npm run dev
php artisan serve
```

### For Laravel 10
Follow the [Laravel 10 installation guide](#laravel-10x-version) below.

## 📸 Screenshots

### Dashboard (Light Mode)
![Dashboard Light](docs/images/dashboard-light.png)

### Dashboard (Dark Mode)  
![Dashboard Dark](docs/images/dashboard-dark.png)

### Mobile Responsive
![Mobile View](docs/images/mobile-view.png)

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

Jikalau kamu ingin tetap menggunakan Breeze 1.19 yg notabene nya masih menggunakan tailwind 3.* maka sebaiknya buka panduan ini untuk melihat panduan ngubah style tailwind v3.* ke tailwind v.4* 
> 📖 **[Lihat Panduan Lengkap Install Breeze 1.19 di laravel 10 dengan upgrade ke style tailwind v4](https://github.com/ahmad-syaifuddin/panduan-install-laravel-breeze-di-laravel10?tab=readme-ov-file#step-5-update-breeze-views-for-tailwind-v4)**

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
use App\Models\User;

class DashboardController extends Controller
{
    public function index()
    {
        // Get dashboard statistics
        $stats = [
            'total_users' => User::count(),
            'active_sessions' => 89, // This would come from sessions table
            'pending_items' => 12,   // This would come from relevant table
            'issues' => 3,           // This would come from issues/tickets table
        ];

        return view('pages.dashboard', compact('stats'));
    }
}
```

## Dashboard Page Example

### Dashboard View (`resources/views/pages/dashboard.blade.php`)

```php
<x-admin title="Dashboard">
    <div class="mb-6">
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white">Dashboard</h1>
        <p class="text-gray-600 dark:text-gray-400">Welcome back! Here's what's happening with your admin panel today.</p>
    </div>
    <!-- Welcome Card -->
            <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg mb-6">
                <div class="p-6 text-gray-900 dark:text-gray-100">
                    <div class="flex items-center space-x-4">
                        <div class="w-12 h-12 bg-primary-500 rounded-full flex items-center justify-center">
                            <i class="fas fa-user text-white"></i>
                        </div>
                        <div>
                            <h3 class="text-xl font-semibold">Welcome back, {{ Auth::user()->name }}! 👋</h3>
                            <p class="text-gray-600 dark:text-gray-400">You're logged in and ready to go.</p>
                        </div>
                    </div>
                </div>
            </div>


    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
        <!-- Stats Cards -->
        <x-card class="text-center">
            <div class="text-3xl font-bold text-primary-600 dark:text-primary-400">{{ $stats['total_users'] ?? 150 }}</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Total Users</div>
            <div class="mt-2">
                <span class="text-xs text-green-600 dark:text-green-400">
                    <i class="fas fa-arrow-up"></i> +12% from last month
                </span>
            </div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-green-600 dark:text-green-400">{{ $stats['active_sessions'] ?? 89 }}</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Active Sessions</div>
            <div class="mt-2">
                <span class="text-xs text-green-600 dark:text-green-400">
                    <i class="fas fa-arrow-up"></i> +5% from yesterday
                </span>
            </div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-yellow-600 dark:text-yellow-400">{{ $stats['pending_items'] ?? 12 }}</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Pending Items</div>
            <div class="mt-2">
                <span class="text-xs text-yellow-600 dark:text-yellow-400">
                    <i class="fas fa-minus"></i> No change
                </span>
            </div>
        </x-card>
        
        <x-card class="text-center">
            <div class="text-3xl font-bold text-red-600 dark:text-red-400">{{ $stats['issues'] ?? 3 }}</div>
            <div class="text-sm text-gray-600 dark:text-gray-400 mt-1">Open Issues</div>
            <div class="mt-2">
                <span class="text-xs text-red-600 dark:text-red-400">
                    <i class="fas fa-arrow-down"></i> -2 from yesterday
                </span>
            </div>
        </x-card>
    </div>
    
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Recent Activity -->
        <x-card title="Recent Activity" subtitle="Latest system activities">
            <div class="space-y-4">
                <div class="flex items-center space-x-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-700">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-green-100 dark:bg-green-900 rounded-full flex items-center justify-center">
                            <i class="fas fa-user-plus text-green-600 dark:text-green-400 text-sm"></i>
                        </div>
                    </div>
                    <div class="flex-1 min-w-0">
                        <p class="text-sm font-medium text-gray-900 dark:text-white">New user registered</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">john.doe@example.com • 2 minutes ago</p>
                    </div>
                </div>
                
                <div class="flex items-center space-x-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-700">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-blue-100 dark:bg-blue-900 rounded-full flex items-center justify-center">
                            <i class="fas fa-edit text-blue-600 dark:text-blue-400 text-sm"></i>
                        </div>
                    </div>
                    <div class="flex-1 min-w-0">
                        <p class="text-sm font-medium text-gray-900 dark:text-white">Settings updated</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">Email notifications enabled • 1 hour ago</p>
                    </div>
                </div>
                
                <div class="flex items-center space-x-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-700">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-red-100 dark:bg-red-900 rounded-full flex items-center justify-center">
                            <i class="fas fa-trash text-red-600 dark:text-red-400 text-sm"></i>
                        </div>
                    </div>
                    <div class="flex-1 min-w-0">
                        <p class="text-sm font-medium text-gray-900 dark:text-white">User account deleted</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">spam.user@example.com • 3 hours ago</p>
                    </div>
                </div>

                <div class="flex items-center space-x-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-700">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-purple-100 dark:bg-purple-900 rounded-full flex items-center justify-center">
                            <i class="fas fa-upload text-purple-600 dark:text-purple-400 text-sm"></i>
                        </div>
                    </div>
                    <div class="flex-1 min-w-0">
                        <p class="text-sm font-medium text-gray-900 dark:text-white">File uploaded</p>
                        <p class="text-xs text-gray-500 dark:text-gray-400">report.pdf • 5 hours ago</p>
                    </div>
                </div>
            </div>
        </x-card>
        
        <!-- Quick Actions -->
        <x-card title="Quick Actions" subtitle="Commonly used admin actions">
            <div class="grid grid-cols-2 gap-4">
                <button class="btn btn-primary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-user-plus"></i>
                    <span>Add User</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-cog"></i>
                    <span>Settings</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-chart-bar"></i>
                    <span>Reports</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-download"></i>
                    <span>Export</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-envelope"></i>
                    <span>Send Mail</span>
                </button>
                
                <button class="btn btn-secondary flex items-center justify-center space-x-2 h-12">
                    <i class="fas fa-database"></i>
                    <span>Backup</span>
                </button>
            </div>
        </x-card>
    </div>

    <!-- System Status -->
    <div class="mt-6">
        <x-card title="System Status" subtitle="Current system health and performance">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="text-center">
                    <div class="text-2xl font-bold text-green-600 dark:text-green-400">99.9%</div>
                    <div class="text-sm text-gray-600 dark:text-gray-400">Uptime</div>
                    <div class="mt-1">
                        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-200">
                            <i class="fas fa-circle w-2 h-2 mr-1"></i>
                            Healthy
                        </span>
                    </div>
                </div>
                
                <div class="text-center">
                    <div class="text-2xl font-bold text-blue-600 dark:text-blue-400">2.3s</div>
                    <div class="text-sm text-gray-600 dark:text-gray-400">Avg Response</div>
                    <div class="mt-1">
                        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-200">
                            <i class="fas fa-circle w-2 h-2 mr-1"></i>
                            Good
                        </span>
                    </div>
                </div>
                
                <div class="text-center">
                    <div class="text-2xl font-bold text-yellow-600 dark:text-yellow-400">76%</div>
                    <div class="text-sm text-gray-600 dark:text-gray-400">Server Load</div>
                    <div class="mt-1">
                        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-200">
                            <i class="fas fa-circle w-2 h-2 mr-1"></i>
                            Moderate
                        </span>
                    </div>
                </div>
            </div>
        </x-card>
    </div>
</x-admin>
```

## Environment Configuration

Create a comprehensive `.env.example` file:

```env
# Application
APP_NAME="Laravel Admin Panel"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

# Logging
LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=admin_panel
DB_USERNAME=root
DB_PASSWORD=

# Broadcasting
BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

# Redis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

# Mail
MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

# AWS (if using S3)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

# Pusher (if using real-time features)
PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

# Vite
VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
```

## Build and Run (Both Versions)

```bash
# Install dependencies
composer install
npm install

# Environment setup
cp .env.example .env
php artisan key:generate

# Configure your database in .env file

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

## 🎨 Customization Guide

### Changing Primary Colors

Update the theme colors in `resources/css/app.css`:

```css
@theme {
  --color-primary: #3b82f6;        /* Change this to your brand color */
  --color-primary-50: #eff6ff;     /* Lightest shade */
  --color-primary-100: #dbeafe;    /* Very light */
  --color-primary-500: #3b82f6;    /* Base color */
  --color-primary-600: #2563eb;    /* Slightly darker */
  --color-primary-700: #1d4ed8;    /* Darker */
  --color-primary-900: #1e3a8a;    /* Darkest shade */
}
```

### Adding New Sidebar Items

Update `resources/views/components/sidebar.blade.php`:

```php
@can('view-analytics')
<li>
    <a href="{{ route('admin.analytics') }}" 
       class="group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold {{ request()->routeIs('admin.analytics') ? 'bg-primary-50 text-primary-600 dark:bg-primary-900/50 dark:text-primary-400' : 'text-gray-700 hover:text-primary-600 hover:bg-gray-50 dark:text-gray-300 dark:hover:text-white dark:hover:bg-gray-700' }}">
        <i class="fas fa-chart-line w-5 h-5 shrink-0"></i>
        Analytics
    </a>
</li>
@endcan
```

### Creating Custom Blade Components

```bash
# Create a new component
php artisan make:component Forms/TextInput
```

Example input component (`resources/views/components/forms/text-input.blade.php`):

```php
@props([
    'label' => '',
    'name' => '',
    'type' => 'text',
    'required' => false,
    'placeholder' => ''
])

<div class="space-y-1">
    @if($label)
        <label for="{{ $name }}" class="block text-sm font-medium text-gray-700 dark:text-gray-300">
            {{ $label }}
            @if($required)
                <span class="text-red-500">*</span>
            @endif
        </label>
    @endif
    
    <input 
        type="{{ $type }}"
        name="{{ $name }}"
        id="{{ $name }}"
        @if($required) required @endif
        @if($placeholder) placeholder="{{ $placeholder }}" @endif
        {{ $attributes->merge(['class' => 'w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-800 dark:border-gray-600 dark:text-white dark:placeholder-gray-400']) }}
    >
    
    @error($name)
        <p class="mt-1 text-sm text-red-600 dark:text-red-400">{{ $message }}</p>
    @enderror
</div>
```

Usage:

```php
<x-forms.text-input 
    label="Email Address" 
    name="email" 
    type="email" 
    :required="true" 
    placeholder="Enter your email"
    value="{{ old('email') }}" 
/>
```

## 🧪 Testing

### Setting up Testing Environment

```bash
# Create test database
php artisan migrate --env=testing

# Run tests
php artisan test

# Run specific test
php artisan test --filter=DashboardTest

# Generate test coverage
php artisan test --coverage
```

### Example Test Cases

```php
// tests/Feature/AdminDashboardTest.php
<?php

namespace Tests\Feature;

use App\Models\User;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;

class AdminDashboardTest extends TestCase
{
    use RefreshDatabase;

    public function test_admin_can_access_dashboard()
    {
        $admin = User::factory()->create(['role' => 'admin']);

        $response = $this->actingAs($admin)->get('/admin/dashboard');

        $response->assertStatus(200);
        $response->assertSee('Dashboard');
    }

    public function test_regular_user_cannot_access_dashboard()
    {
        $user = User::factory()->create(['role' => 'user']);

        $response = $this->actingAs($user)->get('/admin/dashboard');

        $response->assertStatus(403);
    }

    public function test_guest_redirected_to_login()
    {
        $response = $this->get('/admin/dashboard');

        $response->assertRedirect('/login');
    }
}
```

## 📊 Advanced Features

### Adding Real-time Notifications

Install Laravel Echo and Pusher:

```bash
npm install --save-dev laravel-echo pusher-js
```

Update `resources/js/app.js`:

```javascript
import Echo from 'laravel-echo';
import Pusher from 'pusher-js';

window.Pusher = Pusher;

window.Echo = new Echo({
    broadcaster: 'pusher',
    key: import.meta.env.VITE_PUSHER_APP_KEY,
    cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
    forceTLS: true
});

// Listen for notifications
window.Echo.private(`admin.${userId}`)
    .listen('AdminNotification', (e) => {
        // Show notification
        showNotification(e.message, e.type);
    });
```

### Adding Activity Logging

Install Spatie Activity Log:

```bash
composer require spatie/laravel-activitylog
php artisan vendor:publish --provider="Spatie\Activitylog\ActivitylogServiceProvider" --tag="activitylog-migrations"
php artisan migrate
```

Usage in controllers:

```php
use Spatie\Activitylog\Traits\LogsActivity;

class UserController extends Controller
{
    public function store(Request $request)
    {
        $user = User::create($request->validated());
        
        activity()
            ->performedOn($user)
            ->causedBy(auth()->user())
            ->log('Created new user');
            
        return redirect()->route('admin.users');
    }
}
```

### Adding Data Export Features

Create export functionality:

```bash
composer require maatwebsite/excel
php artisan vendor:publish --provider="Maatwebsite\Excel\ExcelServiceProvider" --tag=config
```

Example export class:

```php
// app/Exports/UsersExport.php
<?php

namespace App\Exports;

use App\Models\User;
use Maatwebsite\Excel\Concerns\FromCollection;
use Maatwebsite\Excel\Concerns\WithHeadings;

class UsersExport implements FromCollection, WithHeadings
{
    public function collection()
    {
        return User::select('id', 'name', 'email', 'role', 'created_at')->get();
    }

    public function headings(): array
    {
        return ['ID', 'Name', 'Email', 'Role', 'Created At'];
    }
}
```

Controller method:

```php
use App\Exports\UsersExport;
use Maatwebsite\Excel\Facades\Excel;

public function exportUsers()
{
    return Excel::download(new UsersExport, 'users.xlsx');
}
```

## 🚀 Deployment Guide

### Production Optimization

```bash
# Optimize for production
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan event:cache

# Build production assets
npm run build

# Set proper permissions
chmod -R 755 storage bootstrap/cache
```

### Docker Configuration

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    volumes:
      - .:/var/www/html
    depends_on:
      - db
      - redis
    environment:
      - APP_ENV=production
      - DB_HOST=db
      - REDIS_HOST=redis

  db:
    image: mysql:8.0
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: admin_panel
    volumes:
      - mysql_data:/var/lib/mysql

  redis:
    image: redis:alpine
    ports:
      - "6379:6379"

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
      - .:/var/www/html
    depends_on:
      - app

volumes:
  mysql_data:
```

Create `Dockerfile`:

```dockerfile
FROM php:8.2-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    nodejs \
    npm

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy application code
COPY . .

# Install dependencies
RUN composer install --optimize-autoloader --no-dev
RUN npm install && npm run build

# Set permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port
EXPOSE 8000

# Start PHP-FPM
CMD php artisan serve --host=0.0.0.0 --port=8000
```

### Nginx Configuration

Create `nginx.conf`:

```nginx
server {
    listen 80;
    server_name localhost;
    root /var/www/html/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

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
        <div>
            <h1 class="text-2xl font-bold text-gray-900 dark:text-white">Users</h1>
            <p class="text-gray-600 dark:text-gray-400">Manage system users and their permissions</p>
        </div>
        <button class="btn btn-primary">
            <i class="fas fa-plus mr-2"></i>
            Add User
        </button>
    </div>
    
    <x-card>
        <!-- Your content here -->
        <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
                <thead class="bg-gray-50 dark:bg-gray-800">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Name</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Email</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Role</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Actions</th>
                    </tr>
                </thead>
                <tbody class="bg-white dark:bg-gray-800 divide-y divide-gray-200 dark:divide-gray-700">
                    <!-- Table rows here -->
                </tbody>
            </table>
        </div>
    </x-card>
</x-admin>
```

### Adding New Admin Routes

For Laravel 10, add to `routes/web.php`:
```php
Route::middleware(['auth', 'verified', 'admin'])->prefix('admin')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index'])->name('dashboard');
    Route::resource('/users', UserController::class)->names('admin.users');
    Route::get('/settings', [SettingController::class, 'index'])->name('admin.settings');
    Route::get('/analytics', [AnalyticsController::class, 'index'])->name('admin.analytics');
    Route::post('/users/export', [UserController::class, 'export'])->name('admin.users.export');
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
    'size' => 'md',
    'loading' => false
])

@php
$classes = [
    'primary' => 'btn btn-primary',
    'secondary' => 'btn btn-secondary',
    'danger' => 'bg-red-600 text-white hover:bg-red-700 dark:bg-red-500 dark:hover:bg-red-600',
    'success' => 'bg-green-600 text-white hover:bg-green-700 dark:bg-green-500 dark:hover:bg-green-600',
];

$sizes = [
    'sm' => 'px-3 py-1.5 text-sm',
    'md' => 'px-4 py-2',
    'lg' => 'px-6 py-3 text-lg',
];
@endphp

<button 
    type="{{ $type }}"
    {{ $attributes->merge(['class' => $classes[$variant] . ' ' . $sizes[$size] . ' relative']) }}
    @if($loading) disabled @endif
>
    @if($loading)
        <i class="fas fa-spinner fa-spin mr-2"></i>
    @endif
    {{ $slot }}
</button>
```

Usage:
```php
<x-button variant="primary" size="lg" :loading="false">Save Changes</x-button>
<x-button variant="danger" onclick="confirmDelete()">Delete User</x-button>
```

## Key Differences Between Laravel 10 & 11

| Feature | Laravel 10 | Laravel 11 |
|---------|------------|------------|
| **Middleware Registration** | `app/Http/Kernel.php` | `bootstrap/app.php` |
| **Gates/Policies** | `AuthServiceProvider.php` | `AppServiceProvider.php` |
| **Directory Structure** | Traditional structure | Simplified structure |
| **Service Providers** | Separate Auth provider | Consolidated in App provider |
| **Configuration** | More config files | Streamlined config |
| **PHP Version** | 8.1+ | 8.2+ |
| **Breeze Compatibility** | v1.x (some conflicts) | v2.x (better support) |

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

**6. FontAwesome icons not showing:**
- Ensure `@import "@fortawesome/fontawesome-free/css/all.min.css";` is in `app.css`
- Run `npm install` and `npm run build`

**7. Admin middleware not working:**
- Check middleware registration in correct file (Kernel.php vs bootstrap/app.php)
- Verify user has correct role in database

**8. Gates not working:**
- Ensure gates are defined in correct provider (AuthServiceProvider vs AppServiceProvider)
- Check user is authenticated before testing gates

**9. Dark mode toggle not working:**
- Ensure JavaScript function is loaded
- Check cookie theme value is being set correctly

**10. Permission denied errors:**
```bash
# Fix storage permissions
chmod -R 775 storage bootstrap/cache
chown -R www-data:www-data storage bootstrap/cache
```

### Performance Tips

1. **Production builds:**
   ```bash
   npm run build
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   php artisan event:cache
   ```

2. **Database optimization:**
   ```php
   // Add indexes to frequently queried columns
   Schema::table('users', function (Blueprint $table) {
       $table->index('role');
       $table->index('email');
       $table->index(['role', 'created_at']);
   });
   ```

3. **Cache frequently accessed data:**
   ```php
   // In DashboardController
   public function index()
   {
       $stats = Cache::remember('dashboard.stats', 300, function () {
           return [
               'total_users' => User::count(),
               'active_sessions' => $this->getActiveSessions(),
               'pending_items' => $this->getPendingItems(),
               'issues' => $this->getOpenIssues(),
           ];
       });

       return view('pages.dashboard', compact('stats'));
   }
   ```

4. **Optimize images:**
   - Use optimized avatar images instead of UI Avatars API in production
   - Implement lazy loading for dashboard cards
   - Use WebP format for better compression

## Security Best Practices

### 1. CSRF Protection
Always include CSRF tokens in forms:
```php
<form method="POST" action="{{ route('admin.users.store') }}">
    @csrf
    <!-- form fields -->
</form>
```

### 2. Input Validation
Use Form Requests for complex validation:
```bash
php artisan make:request StoreUserRequest
```

```php
// app/Http/Requests/StoreUserRequest.php
public function rules()
{
    return [
        'name' => 'required|string|max:255',
        'email' => 'required|email|unique:users,email',
        'password' => 'required|string|min:8|confirmed',
        'role' => 'required|in:admin,moderator,user',
    ];
}
```

### 3. Rate Limiting
Add rate limiting to sensitive routes:
```php
Route::middleware(['auth', 'admin', 'throttle:60,1'])->group(function () {
    Route::post('/admin/users', [UserController::class, 'store']);
});
```

### 4. SQL Injection Prevention
Always use Eloquent or query builder:
```php
// Good
User::where('email', $email)->first();

// Bad
DB::select("SELECT * FROM users WHERE email = '$email'");
```

## API Documentation

### Creating API Endpoints

```bash
php artisan make:controller Api/DashboardController
```

```php
// app/Http/Controllers/Api/DashboardController.php
<?php

namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use App\Models\User;

class DashboardController extends Controller
{
    public function stats()
    {
        return response()->json([
            'total_users' => User::count(),
            'active_sessions' => 89,
            'pending_items' => 12,
            'issues' => 3,
        ]);
    }
}
```

Add API routes in `routes/api.php`:
```php
Route::middleware(['auth:sanctum', 'admin'])->prefix('admin')->group(function () {
    Route::get('/stats', [Api\DashboardController::class, 'stats']);
});
```

## Internationalization (i18n)

### Adding Multi-language Support

```bash
php artisan make:middleware SetLocale
```

```php
// app/Http/Middleware/SetLocale.php
public function handle($request, Closure $next)
{
    if (session()->has('locale')) {
        app()->setLocale(session('locale'));
    }
    return $next($request);
}
```

Create language files:
```php
// resources/lang/en/dashboard.php
return [
    'title' => 'Dashboard',
    'welcome' => 'Welcome back!',
    'total_users' => 'Total Users',
    'active_sessions' => 'Active Sessions',
];

// resources/lang/id/dashboard.php
return [
    'title' => 'Dasbor',
    'welcome' => 'Selamat datang kembali!',
    'total_users' => 'Total Pengguna',
    'active_sessions' => 'Sesi Aktif',
];
```

Use in views:
```php
<h1>{{ __('dashboard.title') }}</h1>
<p>{{ __('dashboard.welcome') }}</p>
```

## Contributing

We welcome contributions! Please follow these guidelines:

### 1. Fork and Clone
```bash
git clone https://github.com/your-username/laravel-admin-tailwind4.git
cd laravel-admin-tailwind4
```

### 2. Create Feature Branch
```bash
git checkout -b feature/amazing-feature
```

### 3. Make Changes
- Follow PSR-12 coding standards
- Add tests for new features
- Update documentation

### 4. Test Your Changes
```bash
php artisan test
npm run build
```

### 5. Submit Pull Request
- Write clear commit messages
- Include screenshots for UI changes
- Update CHANGELOG.md

### Code Style Guidelines
```bash
# Install PHP CS Fixer
composer require --dev friendsofphp/php-cs-fixer

# Format code
./vendor/bin/php-cs-fixer fix
```

## Changelog

### v2.0.0 (2024-01-30)
- Added comprehensive documentation
- Added testing examples
- Added deployment guides
- Added Docker configuration
- Enhanced security features
- Added API documentation
- Added internationalization support

### v1.2.0 (2024-01-15)
- Added support for Laravel 11
- Updated middleware registration for Laravel 11
- Consolidated authentication setup

### v1.1.0 (2023-12-20)
- Added dark mode support
- Improved responsive design
- Added flash notification system
- Enhanced dashboard with more statistics

### v1.0.0 (2023-12-01)
- Initial release with Laravel 10 support
- Basic admin panel with Tailwind CSS 4
- Role-based access control
- Modular Blade components

## Roadmap

### v2.1.0 (Planned)
- [ ] Two-factor authentication
- [ ] Advanced user management
- [ ] File manager integration
- [ ] Activity logs viewer
- [ ] System health monitoring

### v2.2.0 (Planned)
- [ ] Advanced reporting features
- [ ] Email template management
- [ ] Backup management interface
- [ ] API rate limiting dashboard
- [ ] Advanced caching controls

### v3.0.0 (Future)
- [ ] Multi-tenancy support
- [ ] Advanced permission system
- [ ] Marketplace for plugins
- [ ] AI-powered analytics
- [ ] Real-time collaboration features

## License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Support

- **Documentation:** This README
- **Issues:** [GitHub Issues](https://github.com/your-username/laravel-admin-tailwind4/issues)
- **Discussions:** [GitHub Discussions](https://github.com/your-username/laravel-admin-tailwind4/discussions)
- **Discord:** [Join our Discord server](https://discord.gg/your-invite)
- **Email:** support@yourdomain.com

### Commercial Support

For commercial support, custom development, or consulting services, please contact us at business@yourdomain.com.

## Credits

- [Laravel](https://laravel.com) - The PHP Framework
- [Tailwind CSS](https://tailwindcss.com) - CSS Framework
- [FontAwesome](https://fontawesome.com) - Icon Library
- [Laravel Breeze](https://laravel.com/docs/starter-kits#laravel-breeze) - Authentication Scaffolding
- [Vite](https://vitejs.dev) - Frontend Build Tool

## Sponsors

Thanks to our sponsors who make this project possible:

- [Your Company Name](https://yourcompany.com)
- [Another Sponsor](https://anothersponsor.com)

### Become a Sponsor

Support this project by becoming a sponsor. Your logo will show up here with a link to your website.

[Become a sponsor on GitHub](https://github.com/sponsors/your-username)
