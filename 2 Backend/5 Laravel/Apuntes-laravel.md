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

### 1. **Generar un Seeder:**

- Abre tu terminal y ejecuta el siguiente comando para crear un seeder. En este ejemplo, usaremos un seeder llamado `UserSeeder`:
    
    ```bash
    php artisan make:seeder UserSeeder
    
    ```
    
- Esto creará un archivo `UserSeeder.php` en el directorio `database/seeders`.

### 2. **Definir la Lógica del Seeder:**

- Abre el archivo `UserSeeder.php` recién creado y modifica el método `run` para insertar datos en tu tabla de usuarios. Puedes usar el Query Builder o Eloquent para hacerlo. Aquí tienes un ejemplo básico utilizando el Query Builder:
    
    ```php
    <?php
     
    namespace Database\Seeders;
     
    use Illuminate\Database\Seeder;
    use Illuminate\Support\Facades\DB;
    use Illuminate\Support\Facades\Hash;
    use Illuminate\Support\Str;
     
    class DatabaseSeeder extends Seeder
    {
        /**
         * Seed the application's database.
         */
        public function run(): void
        {
            {
                DB::table('users')->insert([
                    'name' => Str::random(10),
                    'email' => 'user@user.com',
                    'password' => Hash::make('password'),
                    'role'=>'user'
                ]);
        
                DB::table('users')->insert([
                    'name' => Str::random(10),
                    'email' => 'admin@admin.com',
                    'password' => Hash::make('password'),
                    'role'=>'admin'
                ]);
        
                DB::table('users')->insert([
                    'name' => Str::random(10),
                    'email' => 'super_admin@super_admin.com',
                    'password' => Hash::make('password'),
                    'role'=>'super_admin'
                ]);
            }
        }
    }
    ```
    

### 3. **Generar una Factoría de Modelo:**

- Laravel proporciona factorías para ayudar a generar datos de prueba. Crea una factoría para el modelo `User` ejecutando el siguiente comando:
    
    ```bash
    php artisan make:factory UserFactory
    
    ```
    
- Esto creará un archivo `UserFactory.php` en el directorio `database/factories`.

### 4. **Definir la Factoría:**

- Abre el archivo `UserFactory.php` y define la estructura de los datos que deseas generar. Aquí hay un ejemplo:
    
    ```php
    use Illuminate\\Database\\Eloquent\\Factories\\Factory;
    
    class UserFactory extends Factory
    {
        protected $model = \\App\\Models\\User::class;
    
        public function definition()
        {
            return [
                'name' => $this->faker->name,
                'email' => $this->faker->unique()->safeEmail,
                'password' => bcrypt('password'),
            ];
        }
    }
    
    ```
    

### 5. **Llenar la Base de Datos con Factory:**

- Ahora, puedes utilizar la factoría en tu seeder para llenar la base de datos con múltiples registros. Modifica el método `run` en `UserSeeder.php` para usar la factoría:
    
    ```php
    use App\\Models\\User;
    
    class UserSeeder extends Seeder
    {
        public function run()
        {
            User::factory()->count(10)->create();
        }
    }
    
    ```
    
- Este ejemplo crea 10 usuarios utilizando la factoría.

### 6. **Ejecutar el Seeder:**

- Finalmente, ejecuta el seeder para llenar la base de datos. Utiliza el siguiente comando en la terminal:
    
    ```bash
    php artisan db:seed --class=UserSeeder
    
    ```
    
- Esto ejecutará específicamente el seeder de usuarios.

Ahora deberías tener tu seeder configurado para llenar la base de datos con datos de prueba utilizando la factoría de modelos. Puedes adaptar estos pasos para otros modelos y tablas según tus necesidades.

## Faker para llenar la base de datos

### 1. **Instalar Faker:**

- Abre tu terminal y ejecuta el siguiente comando para instalar la librería Faker:
    
    ```bash
    composer require fzaninotto/faker
    
    ```
    

### 2. **Usar Faker en la Factoría:**

- En tu archivo `UserFactory.php`, utiliza Faker para generar datos más realistas. Asegúrate de importar la clase `Faker` al principio del archivo:
    
    ```php
    use Faker\\Generator as Faker;
    
    ```
    
- Modifica la factoría para utilizar Faker en lugar de datos estáticos:
    
    ```php
    use Illuminate\\Database\\Eloquent\\Factories\\Factory;
    use Faker\\Generator as Faker;
    
    class UserFactory extends Factory
    {
        protected $model = \\App\\Models\\User::class;
    
        public function definition()
        {
            $faker = \\Faker\\Factory::create();
            return [
                'name' => $faker->name,
                'email' => $faker->unique()->safeEmail,
                'password' => bcrypt('password'),
            ];
        }
    }
    
    ```
    

### 3. **Llenar la Base de Datos con Factory y Faker:**

- Ahora, al ejecutar el seeder, los datos serán generados de manera más aleatoria y realista gracias a Faker:
    
    ```bash
    php artisan db:seed --class=UserSeeder
    
    ```
    