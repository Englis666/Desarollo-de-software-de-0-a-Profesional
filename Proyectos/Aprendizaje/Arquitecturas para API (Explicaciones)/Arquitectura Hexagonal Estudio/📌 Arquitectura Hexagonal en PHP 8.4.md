# Introduccion
#PaA
La arquitectura hexagonal (Post and Adapters PaA) busca descaplar la logica de negocio de los detalles de infraestructura, permitiendo que la aplicacion sea flexible y facil de mantener, se divide en:
# Estructura Del Proyecto
```plaintext
	/mi_proyecto/
	│── /backend                 # Carpeta principal del backend
	│   ├── /Config/             # Configuración general (secretKey, .env, etc.)
	│   ├── /public/             # Archivos accesibles públicamente
	│   │   ├── .htaccess        # Reglas de Apache (redirección y seguridad)
	│   │   ├── index.php        # Punto de entrada que redirige a Router.php
	│   ├── /Src/                # Código fuente principal del backend
	│   │   ├── /Application/    # Casos de uso y lógica de aplicación
	│   │   │   ├── /UseCase/    # Clases que implementan los casos de uso
	│   │   ├── /Domain/         # Reglas de negocio y entidades del dominio
	│   │   │   ├── /Entity/     # Modelos que representan los objetos de negocio
	│   │   │   ├── /Repository/ # Interfaces para acceso a datos (Repositories)
	│   │   │   ├── /Service/    # Servicios de dominio (ej. validaciones, cálculos)
	│   │   ├── /Infrastructure/ # Adaptadores para interactuar con sistemas externos
	│   │   │   ├── /Database/   # Configuración y conexión a la base de datos
	│   │   │   ├── /Http/       # Comunicación HTTP (controladores, requests, respuestas)
	│   │   │   │   ├── /Controller/ # Controladores que manejan las peticiones
	│   │   │   │   ├── /Request/    # Validación de datos de entrada (DTOs)
	│   │   │   │   ├── /Response/   # Formateo de respuestas JSON u otras salidas
	│   │   │   │   ├── Router.php   # Definición de rutas y middleware
	│   │   │   ├── /Persistence/    # Implementación de repositorios para DB
	│   │   │   ├── /Security/       # Manejo de autenticación, JWT, roles y permisos
	│── /vendor/                     # Dependencias gestionadas con Composer
	│── composer.json                 # Archivo de configuración de Composer
```


# Backend
	Esta carpeta contiene todo el backend (Logica) del sistema sigueindo una clean Arquitecture con separacion de capas.

# Config 
	Su relevancia es que almacena configuraciones globales (htaccess y index.php env etc) estas afectan al backend como puede ser secret keys o parametros que modifiquen las peticiones entrantes
	**Se recomienda siempre mantener este tipo de configuraciones en una carpeta sola**
# Public 
	Este es el punto de entrada del backend, mayormente contiene los archivos que son habilitados para que sean accedidos por el browser o un cliente (HTTP), eso significa que va a proteger todo el codigo fuente 

# Src 
	Este es el codigo funete principal mayormente es la logica estructurada en capas para escabilidad y mantenimiento
# Application 
#casosDeUsos 
	Aqui mayormente se define que hace el sistema sin necesidad de saber como se implementa (A el que le importa), contiene casos de uso que representan acciones especificas como crear usuario procesar pago listar tareas
# Domain
#modelo
	Representa el corazon del negocio como #entidades, #repositorios, #servicios que definen como funciona el sistema, es completamente idependiente de frameworks y bases de datos
### SubCarpetas
#entidades 
	Esta /Entity que define los objetos del negocio 
#repositorios 
	Interfaces para acceder a datos sin importar de donde viene estos datos
#servicios 
	Logica pura del negocio como validaciones calculos, generacion de tokens
# Infrastructuras 
#baseDeDatos #APis #seguridad 
	Su funcion es interacturar con servicios externos como base de datos o autentificacion, se comunica con **Domain** sin afectar la logica del negocio
### Subcarpetas 
#baseDeDatos 
	/Database Es la conexion y configuracion de la base de datos
	#http
		/Http Es la comunicacion HTTP (Rutas , controladores , validaciones , respuestas)
		#controlador
				//Controller Aqui se recibe las peticiojnes y se llama la capa de application
			#request
				//Request Define las 	reglas de validacion para los datos de entrada
				#response 
				//Response Define la estructura de las respuestas JSON
	#Router
		Router.php Archivo donde se definen las rutas HTTP
	#Persistence 
		/Persistence Implementaciones de repositorios para interacturar con la base de datos
		#security
		/Security Manejo de JWT permisos y seguridades			