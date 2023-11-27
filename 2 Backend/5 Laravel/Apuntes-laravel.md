## Documentación

[Apntes Notion - Bienve](https://www.notion.so/Laravel-ff9f4518b85d44a38d26a1feedc147f4?pvs=21)

[Laravel - The PHP Framework For Web Artisans](https://laravel.com/)

Para crear un proyecto :

```php
composer create-project laravel/laravel primer-proyecto-laravel
```

```php
cd primer-proyecto-laravel
 
php artisan serve
```

→ Vendor es node_modules

→Los tokens ahora son con sanctum, por lo que habrá que descargarla e instalarla

```php
php artisan 
```

Estecomando te indicará todos los comandos que hay.

## Comandos básicos

1. **Instalar Laravel:**
    
    ```bash
    composer create-project --prefer-dist laravel/laravel nombre-de-tu-proyecto
    
    ```
    
    Este comando crea un nuevo proyecto Laravel en un directorio llamado `nombre-de-tu-proyecto`. Asegúrate de tener Composer instalado antes de ejecutar este comando.
    
2. **Crear un controlador:**
    
    ```bash
    php artisan make:controller NombreDelControlador
    ```
    
    Esto generará un nuevo controlador en el directorio `app/Http/Controllers`.
    
3. **Crear un modelo:**
    
    ```bash
    php artisan make:model NombreDelModelo
    ```
    
    Este comando generará un nuevo modelo en el directorio `app/Models`.
    
4. **Crear una migración para el modelo:**
    
    ```bash
    php artisan make:migration nombre_de_la_migracion
    ```
    
    Las migraciones se utilizan para definir la estructura de la base de datos. Después de crear la migración, puedes modificar el archivo generado en el directorio `database/migrations` según tus necesidades y luego ejecutar las migraciones para aplicar los cambios a la base de datos:
    
    ```bash
    php artisan migrate
    ```
    
5. **Crear un recurso (Resource) para la API:**
    
    ```bash
    php artisan make:resource NombreDelRecurso
    ```
    
    Los recursos son útiles para transformar datos y enviar respuestas estructuradas desde tu API.
    
6. **Crear una ruta en el archivo de rutas (routes/web.php o routes/api.php):**
Por ejemplo, en `routes/web.php` o `routes/api.php`, puedes agregar una ruta que apunte a un controlador y un método específicos:
    
    ```php
    Route::get('/ruta', 'NombreDelControlador@metodo');
    
    ```
    
7. **Ejecutar el servidor de desarrollo:**
    
    ```bash
    php artisan serve
    
    ```
    
    Esto inicia el servidor de desarrollo. Puedes acceder a tu aplicación en `http://localhost:8000`.
    
8. **Generar un recurso de controlador (Controller Resource):**
    
    ```bash
    php artisan make:controller NombreDelControlador --resource
    
    ```
    
    Esto generará un controlador con métodos de recursos que puedes utilizar para las operaciones CRUD (Crear, Leer, Actualizar, Eliminar).
    

Estos son solo algunos de los comandos básicos que puedes utilizar en Laravel. La documentación oficial de Laravel (https://laravel.com/docs) es una excelente fuente de referencia para obtener más información sobre cómo trabajar con el framework y sus numerosas características.

<aside>
📌 Bootstrap no tiene nada que ver con el diseño… es un  punto de entrada. Lo que voy a ejecutar para que funciona mi app.

</aside>

<aside>
📌 El arvhivo database.php no se toca. Porque en el archivo .env es donde se configura tu BBDD

</aside>

Para poder customizar los errores debe ser desde views→(carpeta)errors→(archivo)404.blade.php

```bash
php artisan migrate
```

```bash
php artisan migrate:rollback
```