---
title: Cómo estructurar un proyecto con Laravel desde cero
date: 2024/11/28
description: Aprende cómo estructurar un proyecto desde cero con Laravel, desde la instalación y configuración inicial hasta la creación de rutas, controladores y vistas. Una guía práctica para desarrollar aplicaciones web escalables y organizadas.
tag: Laravel, PHP
author: Farley Piedrahita Orozco
---

Laravel es un framework PHP poderoso y flexible que permite desarrollar aplicaciones web de manera rápida y organizada. En este post, te guiaré paso a paso para estructurar un proyecto desde cero y asegurarte de que esté listo para crecer de forma escalable y mantenible.  

---

#### **1. Instalación de Laravel**  
Antes de empezar, asegúrate de que tienes instalado:  
- PHP (versión 8.0 o superior)  
- Composer (gestor de dependencias de PHP)  
- Un servidor web como Apache o Nginx  
- MySQL o cualquier otra base de datos que prefieras  

**Paso 1:** Instala Laravel utilizando Composer.  
```bash  
composer create-project laravel/laravel nombre-proyecto  
```  
Esto creará una carpeta llamada `nombre-proyecto` con la estructura básica de Laravel.  

**Paso 2:** Accede al directorio del proyecto y levanta el servidor de desarrollo.  
```bash  
cd nombre-proyecto  
php artisan serve  
```  
Esto inicia el servidor local en `http://localhost:8000`.  

---

#### **2. Conoce la estructura de carpetas de Laravel**  

La estructura de un proyecto Laravel es clave para organizar el desarrollo:  

- **`app/`**: Contiene la lógica principal de la aplicación (controladores, modelos, servicios).  
- **`routes/`**: Define las rutas de la aplicación.  
- **`resources/`**: Contiene vistas, archivos CSS/JS, y otros recursos estáticos.  
- **`database/`**: Aquí encontrarás las migraciones, factories y seeders.  
- **`config/`**: Archivos de configuración del proyecto.  
- **`public/`**: Carpeta pública donde se sirven los recursos accesibles al navegador.  

---

#### **3. Configuración básica del proyecto**  

1. **Configura el archivo `.env`**  
   Este archivo define variables de entorno, como la conexión a la base de datos:  
   ```env  
   APP_NAME=MiAplicacion  
   APP_URL=http://localhost:8000  
   DB_CONNECTION=mysql  
   DB_HOST=127.0.0.1  
   DB_PORT=3306  
   DB_DATABASE=nombre_base_datos  
   DB_USERNAME=usuario  
   DB_PASSWORD=contraseña  
   ```  

2. **Genera la clave de la aplicación**  
   Ejecuta este comando para generar una clave de seguridad única:  
   ```bash  
   php artisan key:generate  
   ```  

---

#### **4. Crear las rutas iniciales**  
Laravel utiliza el archivo `routes/web.php` para definir las rutas de la aplicación web.  
Ejemplo de una ruta básica:  
```php  
Route::get('/', function () {  
    return view('welcome');  
});  
```  

Para organizar mejor las rutas, puedes agruparlas o asignar controladores.  
```php  
Route::prefix('admin')->group(function () {  
    Route::get('/dashboard', [AdminController::class, 'dashboard']);  
});  
```  

---

#### **5. Crear un controlador y su lógica básica**  
Laravel utiliza controladores para manejar la lógica de las rutas.  
**Paso 1:** Genera un controlador.  
```bash  
php artisan make:controller HomeController  
```  
Esto crea `app/Http/Controllers/HomeController.php`.  

**Paso 2:** Añade una función al controlador.  
```php  
namespace App\Http\Controllers;  

use Illuminate\Http\Request;  

class HomeController extends Controller  
{  
    public function index()  
    {  
        return view('home');  
    }  
}  
```  

**Paso 3:** Asocia el controlador a una ruta.  
```php  
Route::get('/home', [HomeController::class, 'index']);  
```  

---

#### **6. Configura la base de datos**  

1. **Crea una migración para tu tabla**  
   ```bash  
   php artisan make:migration create_posts_table  
   ```  
   Edita el archivo generado en `database/migrations` para definir la estructura:  
   ```php  
   Schema::create('posts', function (Blueprint $table) {  
       $table->id();  
       $table->string('title');  
       $table->text('content');  
       $table->timestamps();  
   });  
   ```  

2. **Ejecuta las migraciones**  
   ```bash  
   php artisan migrate  
   ```  

3. **Crea un modelo asociado**  
   ```bash  
   php artisan make:model Post  
   ```  
   El modelo se utiliza para interactuar con la base de datos.  

---

#### **7. Diseña una vista básica**  

Las vistas se encuentran en `resources/views`. Crea un archivo `home.blade.php`:  
```html  
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Home</title>  
</head>  
<body>  
    <h1>¡Bienvenido a mi aplicación Laravel!</h1>  
</body>  
</html>  
```  

---

#### **8. Pruebas rápidas del proyecto**  

1. **Prueba las rutas:**  
   Ve a `http://localhost:8000/home` y verifica que la vista se muestra correctamente.  

2. **Prueba la base de datos:**  
   Usa Tinker para interactuar con los modelos.  
   ```bash  
   php artisan tinker  
   >>> Post::create(['title' => 'Mi primer post', 'content' => 'Contenido del post']);  
   >>> Post::all();  
   ```  

---

#### **9. Mejora y expande tu proyecto**  

- **Middleware:** Usa middleware para manejar la autenticación o la validación de solicitudes.  
- **Autenticación:** Configura un sistema de autenticación con `php artisan make:auth` o Jetstream.  
- **API:** Agrega endpoints RESTful con controladores API.  

---

Con estos pasos, ya cuentas con una base sólida para iniciar cualquier proyecto en Laravel. Si te gustaría profundizar en algún tema, no dudes en escribirme a farchodev@gmail.com. ¡Estaré encantado de ayudarte! 😊