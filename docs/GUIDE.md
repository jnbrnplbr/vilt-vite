1. Install Laravel 
```php
      // 1. create new laravel
      laravel new isi-website

      // 2. create .env file
      cp .env.example

      // 3. generate key
      php artisan key:generate
```

2. Install inertiajs dependencies for Laravel
```php
      composer require inertiajs/inertia-laravel
```

3. Add layout template (not necessary). I created resources/views/app.blade.php

```html
<!DOCTYPE html>
<html>
      <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
            
            <!-- FOR LARAVEL MIX YOU THIS: -->
            <!-- 
                  <link href="{{ mix('/css/app.css') }}" rel="stylesheet" />
            <script src="{{ mix('/js/app.js') }}" defer></script> 
            -->  

            <!-- FOR VITE YOU THIS: -->
            @vite(['resources/css/app.css', 'resources/js/app.js'])

            @inertiaHead
      </head>
      <body>
            @inertia
      </body>
</html>
```

4. Setup the initial middleware.
```php
      php artisan inertia:middleware
```

5. Register to the Kernel class, on web middleware group.
```php
      // app/Http/Kernel.php
      // add only on the web middleware group
      'web' => [
            \App\Http\Middleware\HandleInertiaRequests::class, 
      ];
      
```

6. Install Client Side Dependencies for VueJS3 
```php
      npm install @inertiajs/inertia @inertiajs/inertia-vue3
```


7. Install vue
```php
      npm install vue@next
```

8. Install Single File Component (not necessary)
```php
      npm install -D @vue/compiler-sfc
```

9. Initialize your App. 
```js
      // inside resources/js/app.js paste the code below (initially theres a import ../boostrap which we can remove for now)
      
      import { createApp, h } from 'vue'
      import { createInertiaApp } from '@inertiajs/inertia-vue3'
      import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';  // for vite
      import '../css/app.css'; // for vite

      createInertiaApp({
      // resolve: name => require(`./Pages/${name}`),                                     // For webpack, laravel-mix
      resolve: (name) => resolvePageComponent(`./Pages/${name}.vue`, import.meta.glob('./Pages/**/*.vue')), // For vite
      setup({ el, App, props, plugin }) {
            createApp({ render: () => h(App, props) })
                  .use(plugin)
                  .mount(el)
            },
      })

      // Add Pages directory inside the resources/js (can be done manually or via cmd)
      mkdir resources/js/Pages 

```

10. You can now start the application:
```php
      npm run dev
```


### Errors you might encounter 

```php
      // some errors that may occur: 
      // 1. cannot find module path : node:path
      fix will be update your node version 
      

      // 2. Error: Cannot find module '@vitejs/plugin-vue'
      npm install @vitejs/plugin-vue

```

