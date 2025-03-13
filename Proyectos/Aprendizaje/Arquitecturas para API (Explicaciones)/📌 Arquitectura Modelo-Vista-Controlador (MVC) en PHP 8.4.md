## 📖 Introducción
#MVC 
El patrón **Modelo-Vista-Controlador (MVC)** separa la lógica de la aplicación en tres componentes:

- **Modelo (Model):** Gestiona los datos y la lógica de negocio.
- **Vista (View):** Maneja la presentación y la interfaz de usuario.
- **Controlador (Controller):** Procesa las solicitudes y enlaza el modelo con la vista.

## 📂 Estructura del Proyecto
#estructuras

```plaintext
/mi_proyecto/
│── /App/
│   ├── /Controllers/
│   ├── /Models/
│   ├── /Views/
│   ├── /Core/
│   ├── /Config/
│── /Public/
│   ├── index.php
│── /Storage/
│── /Vendor/  (Composer)
│── composer.json
```

## 🚀 Configuración del Front Controller

**Archivo:** `/Public/index.php`

```php
<?php

use App\Core\Router;

require_once __DIR__ . '/../vendor/autoload.php';

session_start();

require_once __DIR__ . '/../App/Config/config.php';

$router = new Router();
$router->dispatch($_SERVER['REQUEST_URI']);
```

## 🔹 Enrutador Personalizado

**Archivo:** `/App/Core/Router.php`

```php
<?php

namespace App\Core;

class Router {
    private array $routes = [];

    public function __construct() {
        $this->routes = require __DIR__ . '/../Config/routes.php';
    }

    public function dispatch(string $uri) {
        $uri = trim(parse_url($uri, PHP_URL_PATH), '/');

        if (array_key_exists($uri, $this->routes)) {
            [$controller, $method] = explode('@', $this->routes[$uri]);
            $controller = "App\\Controllers\\$controller";
            if (class_exists($controller) && method_exists($controller, $method)) {
                call_user_func([new $controller, $method]);
                return;
            }
        }

        http_response_code(404);
        echo "Página no encontrada";
    }
}
```

**Archivo:** `/App/Config/routes.php`

```php
<?php

return [
    '' => 'HomeController@index',
    'productos' => 'ProductoController@index',
    'productos/ver' => 'ProductoController@ver',
];
```

## 🔹 Controladores

**Archivo:** `/App/Controllers/HomeController.php`

```php
<?php

namespace App\Controllers;

use App\Core\View;

class HomeController {
    public function index() {
        return View::render('home', ['titulo' => 'Bienvenido a PHP 8.4']);
    }
}
```

## 🔹 Modelos

**Archivo:** `/App/Models/Producto.php`

```php
<?php

namespace App\Models;

use App\Core\Database;

class Producto {
    protected Database $db;

    public function __construct() {
        $this->db = new Database();
    }

    public function obtenerTodos(): array {
        return $this->db->query("SELECT * FROM productos")->fetchAll();
    }
}
```

## 🔹 Vistas

**Archivo:** `/App/Views/home.php`

```php
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title><?= $titulo ?? 'Mi Sitio' ?></title>
</head>
<body>
    <h1><?= $titulo ?? 'Bienvenido' ?></h1>
</body>
</html>
```

**Archivo:** `/App/Core/View.php`

```php
<?php

namespace App\Core;

class View {
    public static function render(string $vista, array $datos = []) {
        extract($datos);
        require __DIR__ . "/../Views/$vista.php";
    }
}
```

## 🔥 Base de Datos con PDO
#baseDeDatos #db #PDO

**Archivo:** `/App/Core/Database.php`

```php
<?php

namespace App\Core;

use PDO;
use PDOException;

class Database {
    private PDO $pdo;

    public function __construct() {
        $config = require __DIR__ . '/../Config/database.php';
        $dsn = "mysql:host={$config['host']};dbname={$config['dbname']};charset=utf8mb4";

        try {
            $this->pdo = new PDO($dsn, $config['user'], $config['password'], [
                PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
            ]);
        } catch (PDOException $e) {
            die("Error de conexión: " . $e->getMessage());
        }
    }

    public function query(string $sql) {
        return $this->pdo->query($sql);
    }
}
```

**Archivo:** `/App/Config/database.php`

```php
<?php

return [
    'host' => 'localhost',
    'dbname' => 'mi_base_de_datos',
    'user' => 'root',
    'password' => '',
];
```

## ✅ Conclusión

	Este es un ejemplo básico de cómo estructurar un proyecto MVC en PHP 8.4 de manera modular y limpia. Puedes expandirlo agregando:

- Middleware para autenticación y seguridad. #Middleware
- Un sistema de plantillas como Blade o Twig. #Blade #Twing 
- Integración con APIs RESTful. #APIRESTFULL
