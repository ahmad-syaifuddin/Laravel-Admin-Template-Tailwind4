# Laravel + Tailwind 4 Admin Panel Starter Kit

🚀 **Panduan lengkap setup Laravel dengan Tailwind CSS 4 untuk membuat Admin Panel modern dengan Dark Mode support**

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Setup Tailwind 4](#setup-tailwind-4)
- [Dark Mode Configuration](#dark-mode-configuration)
- [Admin Layout Structure](#admin-layout-structure)
- [Components Best Practices](#components-best-practices)
- [Responsive Design](#responsive-design)
- [Performance Optimization](#performance-optimization)
- [Troubleshooting](#troubleshooting)

## Prerequisites

- PHP 8.1+ (untuk Laravel 10+) atau PHP 8.2+ (untuk Laravel 11+)
- Node.js 18+
- Composer 2.0+
- Laravel 10+ (recommended Laravel 11 untuk fitur terbaru)

### Compatibility Matrix

| Laravel Version | PHP Version | Tailwind 4 Support | Vite Version |
|----------------|-------------|-------------------|--------------|
| 11.x           | PHP 8.2+    | ✅ Full Support   | 5.0+         |
| 10.x           | PHP 8.1+    | ✅ Full Support   | 4.0+         |
| 9.x            | PHP 8.0+    | ⚠️ Manual Setup   | 3.0+         |

## Installation

### 1. Create New Laravel Project

#### Opsi A: Menggunakan Laravel Installer

```bash
# Install Laravel installer (jika belum ada)
composer global require laravel/installer

# Membuat project dengan versi terbaru (Laravel 11.x)
laravel new admin-panel
cd admin-panel

# ⚠️ Note: Laravel Installer 5.16.0+ hanya support Laravel versi terbaru
# Untuk versi spesifik, gunakan Composer (lihat Opsi B)
```

#### Opsi B: Menggunakan Composer Create-Project (Recommended untuk versi spesifik)

```bash
# Versi terbaru (stable)
composer create-project laravel/laravel admin-panel

# ✅ Laravel 10 (LTS) - RECOMMENDED
composer create-project laravel/laravel admin-panel "10.*"

# ✅ Laravel 9 (jika masih diperlukan)
composer create-project laravel/laravel admin-panel "^9.0"

# Versi spesifik
composer create-project laravel/laravel admin-panel "10.48.22"

# Dengan dev dependencies
composer create-project laravel/laravel admin-panel "^10.0" --prefer-dist

cd admin-panel
```

#### Opsi C: Clone dari GitHub (Alternative)

```bash
# Clone repository Laravel
git clone https://github.com/laravel/laravel.git admin-panel
cd admin-panel

# Checkout ke tag versi tertentu
git checkout v10.4.1

# Install dependencies
composer install
cp .env.example .env
php artisan key:generate
```

#### Opsi D: Cek Versi Available

```bash
# Cek versi Laravel yang tersedia
composer show laravel/laravel --available

# Atau cek versi framework
composer show laravel/framework --available

# Cek versi Laravel Installer yang terinstall
laravel --version

# Update Laravel Installer ke versi terbaru
composer global update laravel/installer
```

#### ⚡ Quick Commands untuk Versi Populer

```bash
# Laravel 11.x (Latest - PHP 8.2+)
composer create-project laravel/laravel admin-panel

# Laravel 10.x (LTS - PHP 8.1+)
composer create-project laravel/laravel admin-panel "^10.0"

# Laravel 9.x (PHP 8.0+)
composer create-project laravel/laravel admin-panel "^9.0"
```

### 2. Install Tailwind CSS 4

```bash
# Install Tailwind 4 dan dependensinya
npm install tailwindcss @tailwindcss/vite

# Untuk Laravel 9.x atau versi lama (manual setup)
npm install tailwindcss @tailwindcss/vite postcss autoprefixer

# Verify installation
npm list tailwindcss
```

#### Note untuk Laravel versi lama:
Jika menggunakan Laravel 9.x atau dibawah, mungkin perlu setup manual PostCSS:

```bash
# Generate postcss.config.js (jika belum ada)
npx tailwindcss init -p
```

### 3. Configure Vite

Edit `vite.config.js`:

```javascript
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'
import laravel from 'laravel-vite-plugin'

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        tailwindcss(),
    ],
})
```

## Setup Tailwind 4

### 1. Configure CSS

Edit `resources/css/app.css`:

```css
@import "tailwindcss";

/* Scan Laravel views directory */
@source "../views";

/* Custom CSS untuk Admin Panel */
@layer base {
    html {
        scroll-behavior: smooth;
    }
    
    body {
        @apply antialiased;
    }
}

@layer components {
    /* Button Components */
    .btn {
        @apply px-4 py-2 rounded-lg font-medium transition-all duration-200;
    }
    
    .btn-primary {
        @apply bg-blue-600 text-white hover:bg-blue-700 focus:ring-4 focus:ring-blue-200 dark:focus:ring-blue-800;
    }
    
    .btn-secondary {
        @apply bg-gray-200 text-gray-800 hover:bg-gray-300 dark:bg-gray-700 dark:text-gray-200 dark:hover:bg-gray-600;
    }
    
    .btn-danger {
        @apply bg-red-600 text-white hover:bg-red-700 focus:ring-4 focus:ring-red-200 dark:focus:ring-red-800;
    }
    
    /* Card Components */
    .card {
        @apply bg-white dark:bg-gray-800 rounded-lg shadow-sm border border-gray-200 dark:border-gray-700;
    }
    
    .card-header {
        @apply px-6 py-4 border-b border-gray-200 dark:border-gray-700;
    }
    
    .card-body {
        @apply p-6;
    }
    
    /* Form Components */
    .form-input {
        @apply w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:focus:ring-blue-400;
    }
    
    .form-label {
        @apply block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2;
    }
    
    /* Sidebar */
    .sidebar-link {
        @apply flex items-center px-4 py-3 text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg transition-colors duration-200;
    }
    
    .sidebar-link.active {
        @apply bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300;
    }
}

@layer utilities {
    .text-balance {
        text-wrap: balance;
    }
    
    .scrollbar-hide {
        -ms-overflow-style: none;
        scrollbar-width: none;
    }
    
    .scrollbar-hide::-webkit-scrollbar {
        display: none;
    }
}
```

## Dark Mode Configuration

### 1. Setup Custom Dark Mode Selector

Tambahkan custom variant di `resources/css/app.css`:

```css
@import "tailwindcss";
@source "../views";

/* Custom dark mode variant */
@custom-variant dark (&:where(.dark, .dark *));
```

### 2. Dark Mode Toggle Script

Buat file `resources/js/darkmode.js`:

```javascript
// Dark mode toggle functionality
function initDarkMode() {
    // Check if dark mode is enabled on page load
    if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
        document.documentElement.classList.add('dark')
    } else {
        document.documentElement.classList.remove('dark')
    }
}

function toggleDarkMode() {
    if (document.documentElement.classList.contains('dark')) {
        document.documentElement.classList.remove('dark')
        localStorage.theme = 'light'
    } else {
        document.documentElement.classList.add('dark')
        localStorage.theme = 'dark'
    }
}

// Initialize dark mode on page load
document.addEventListener('DOMContentLoaded', initDarkMode)

// Make functions available globally
window.toggleDarkMode = toggleDarkMode
```

Import di `resources/js/app.js`:

```javascript
import './bootstrap'
import './darkmode'
```

## Admin Layout Structure

### 1. Main Layout - `resources/views/layouts/admin.blade.php`

```blade
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}" class="h-full">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="csrf-token" content="{{ csrf_token() }}">
    
    <title>@yield('title', 'Admin Panel')</title>
    
    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
<body class="h-full bg-gray-50 dark:bg-gray-900">
    <div class="flex h-full">
        <!-- Sidebar -->
        @include('layouts.partials.sidebar')
        
        <!-- Main Content -->
        <div class="flex-1 flex flex-col overflow-hidden">
            <!-- Header -->
            @include('layouts.partials.header')
            
            <!-- Main Content Area -->
            <main class="flex-1 overflow-y-auto p-6">
                @yield('content')
            </main>
        </div>
    </div>
    
    <!-- Dark mode toggle script -->
    <script>
        // Prevent FOUC (Flash of Unstyled Content)
        (function() {
            if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark')
            }
        })()
    </script>
</body>
</html>
```

### 2. Sidebar - `resources/views/layouts/partials/sidebar.blade.php`

```blade
<div class="w-64 bg-white dark:bg-gray-800 shadow-lg flex flex-col">
    <!-- Logo -->
    <div class="p-6 border-b border-gray-200 dark:border-gray-700">
        <h1 class="text-xl font-bold text-gray-900 dark:text-white">
            Admin Panel
        </h1>
    </div>
    
    <!-- Navigation -->
    <nav class="flex-1 p-4 space-y-2">
        <a href="{{ route('admin.dashboard') }}" 
           class="sidebar-link {{ request()->routeIs('admin.dashboard') ? 'active' : '' }}">
            <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                      d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2H5a2 2 0 00-2-2z"/>
            </svg>
            Dashboard
        </a>
        
        <a href="{{ route('admin.users') }}" 
           class="sidebar-link {{ request()->routeIs('admin.users*') ? 'active' : '' }}">
            <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                      d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"/>
            </svg>
            Users
        </a>
        
        <a href="{{ route('admin.settings') }}" 
           class="sidebar-link {{ request()->routeIs('admin.settings*') ? 'active' : '' }}">
            <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                      d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
            </svg>
            Settings
        </a>
    </nav>
</div>
```

### 3. Header - `resources/views/layouts/partials/header.blade.php`

```blade
<header class="bg-white dark:bg-gray-800 shadow-sm border-b border-gray-200 dark:border-gray-700">
    <div class="flex items-center justify-between px-6 py-4">
        <!-- Page Title -->
        <div>
            <h2 class="text-xl font-semibold text-gray-800 dark:text-white">
                @yield('page-title', 'Dashboard')
            </h2>
        </div>
        
        <!-- Header Actions -->
        <div class="flex items-center space-x-4">
            <!-- Dark Mode Toggle -->
            <button onclick="toggleDarkMode()" 
                    class="p-2 rounded-lg text-gray-500 hover:text-gray-700 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-200 dark:hover:bg-gray-700 transition-colors">
                <svg class="w-5 h-5 hidden dark:block" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                          d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"/>
                </svg>
                <svg class="w-5 h-5 block dark:hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                          d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"/>
                </svg>
            </button>
            
            <!-- User Dropdown -->
            <div class="relative">
                <button class="flex items-center space-x-2 text-gray-700 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white">
                    <img class="w-8 h-8 rounded-full" src="https://ui-avatars.com/api/?name={{ auth()->user()->name ?? 'Admin' }}&background=3b82f6&color=fff" alt="Avatar">
                    <span class="text-sm font-medium">{{ auth()->user()->name ?? 'Admin' }}</span>
                </button>
            </div>
        </div>
    </div>
</header>
```

## Components Best Practices

### 1. Data Table Component

```blade
{{-- resources/views/components/data-table.blade.php --}}
<div class="card">
    <div class="card-header">
        <h3 class="text-lg font-medium text-gray-900 dark:text-white">{{ $title }}</h3>
    </div>
    <div class="overflow-x-auto">
        <table class="w-full divide-y divide-gray-200 dark:divide-gray-700">
            <thead class="bg-gray-50 dark:bg-gray-700">
                {{ $header }}
            </thead>
            <tbody class="bg-white dark:bg-gray-800 divide-y divide-gray-200 dark:divide-gray-700">
                {{ $slot }}
            </tbody>
        </table>
    </div>
</div>
```

### 2. Form Components

```blade
{{-- resources/views/components/form-input.blade.php --}}
<div class="mb-4">
    @if($label)
        <label for="{{ $id }}" class="form-label">{{ $label }}</label>
    @endif
    <input 
        type="{{ $type ?? 'text' }}" 
        id="{{ $id }}"
        name="{{ $name }}"
        class="form-input {{ $errors->has($name) ? 'border-red-500 focus:border-red-500 focus:ring-red-500' : '' }}"
        value="{{ $value ?? old($name) }}"
        {{ $attributes }}
    >
    @error($name)
        <p class="mt-1 text-sm text-red-600 dark:text-red-400">{{ $message }}</p>
    @enderror
</div>
```

## Responsive Design

### Mobile-First Approach

```css
/* Responsive sidebar */
@media (max-width: 768px) {
    .sidebar {
        @apply -translate-x-full fixed inset-y-0 z-50 w-64 transition-transform;
    }
    
    .sidebar.open {
        @apply translate-x-0;
    }
    
    .main-content {
        @apply ml-0;
    }
}

/* Responsive tables */
@media (max-width: 640px) {
    .responsive-table {
        @apply text-sm;
    }
    
    .responsive-table th:not(:first-child):not(:last-child) {
        @apply hidden;
    }
    
    .responsive-table td:not(:first-child):not(:last-child) {
        @apply hidden;
    }
}
```

## Performance Optimization

### 1. Build Process

```bash
# Development
npm run dev

# Production build
npm run build
```

### 2. CSS Optimization

Di production, Tailwind 4 secara otomatis menghapus unused CSS. Pastikan build process berjalan dengan baik:

```javascript
// vite.config.js untuk production
export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        tailwindcss(),
    ],
    build: {
        rollupOptions: {
            output: {
                manualChunks: {
                    vendor: ['alpinejs']
                }
            }
        }
    }
})
```

## Troubleshooting

### Common Issues

1. **Styles tidak muncul**
   - Pastikan `@vite` directive sudah benar di layout
   - Jalankan `npm run dev` atau `npm run build`
   - Clear browser cache

2. **Dark mode tidak berfungsi**
   - Periksa JavaScript untuk dark mode toggle
   - Pastikan custom variant sudah dikonfigurasi
   - Check localStorage di browser dev tools

3. **Build error**
   ```bash
   # Clear node modules dan reinstall
   rm -rf node_modules package-lock.json
   npm install
   ```

4. **Laravel version compatibility issues**
   ```bash
   # Check Laravel version
   php artisan --version
   
   # Check if Vite is available (Laravel 9.19+)
   php artisan list | grep vite
   
   # Jika tidak ada Vite, upgrade Laravel atau gunakan Laravel Mix
   composer update laravel/framework
   ```

5. **PHP version mismatch**
   ```bash
   # Check current PHP version
   php -v
   
   # Check composer.json requirements
   cat composer.json | grep php
   
   # Update PHP if needed (Ubuntu/Debian example)
   sudo apt update
   sudo apt install php8.2-cli php8.2-fpm
   ```

### Performance Tips

- Gunakan `@apply` directive dengan hati-hati di production
- Manfaatkan component classes untuk styling yang berulang
- Optimasi gambar dan aset statis
- Gunakan CDN untuk aset yang besar

## Best Practices Checklist

- ✅ Gunakan semantic HTML
- ✅ Implement proper color contrast untuk accessibility  
- ✅ Mobile-first responsive design
- ✅ Dark mode support
- ✅ Consistent component structure
- ✅ Performance optimization
- ✅ Clean and maintainable CSS
- ✅ Proper error handling
- ✅ SEO-friendly markup
- ✅ Cross-browser compatibility

## Useful Resources

- [Tailwind CSS 4 Documentation](https://tailwindcss.com/docs)
- [Laravel Documentation](https://laravel.com/docs)
- [Vite Documentation](https://vitejs.dev/)
- [Heroicons](https://heroicons.com/) - SVG icons
- [Headless UI](https://headlessui.com/) - Unstyled components

---

**Happy coding! 🚀**

> Panduan ini akan terus diupdate seiring dengan perkembangan Tailwind CSS 4 dan Laravel.
