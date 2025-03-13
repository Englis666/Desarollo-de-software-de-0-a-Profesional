#container
Es un sistema que automatiza la inyeccion de dependencias

	Entonces en ves de crear los objetos con new, el contenedor se encarga de crearlos y pasarlos automaticamente a las clases que los necesitan

- **Esto ayuda mucho para evitar depedencias con otras**

	Esto es un contenedor aqui es el PHP-DI (Dependency Injection)
	
		$container = new Container();
		
	Ahora se lo va a a pasar a **Slim** para que lo pueda usar internamente.
	
		AppFactory::setContainer($container);
	 
# Manejo de la base de datos

#container #db 
	El contenedor (Container) en la estructura hexagonal se utiliza para almacenar la db ya que es la metologia

		$caonteiner->set('db', function () {
			return New PDO("mysql:host=localhost;dbname=tabla", "root" , "" );
		});
 - **Se guarda la conexion a la base de datos dentro del contenedor con la clave 'db' **
 - **Cuando alguien llame a $container->get('db') , obtendra la conexion de base de datos sin necesidad de crearla de nuevo**
# UserRepositoryImpl en el contenedor

	$container->set(UserRepositoryImpl::class, function ($c) {
	    return new UserRepositoryImpl($c->get('db'));
	});
- **Se le dice al contenedor:
	"Cada vez que alguien necesite `UserRepositoryImpl`, crea una nueva instancia y pásale la conexión a la base de datos (`$c->get('db')`)." **
-  **$c representa el contenedor por eso se usa $c->get('db') para recuperar la conexion en este caso** 

### Donde se usa?
	Esta ubicada en la capa de infraestructura (Infrastructure) porque se implementa como se guardan y se recuperan los datos

		La capa de aplicacion no sabe ni le importa si la base de datos es MySQL , Mongo o un archivo. Solo usa Userrepository que es una interfaz


# RegisterUser en el contenedor

$container->set(RegisterUser::class, function ($c) {
    return new RegisterUser($c->get(UserRepositoryImpl::class));
});

RegisterUser es un #casosDeUsos (Capa de aplicacion), que maneja la logica del negocio del registro
Este recibe UserRepositoryImpl como depdencia porque necesita acceder a los usuarios
En vez de crear manualmente new RegisterUser(New UserRepositoryImpl($db)) se utiliza el contenedor para hacerlo mas sencillo

# AuthController en el contenedor

$container->set(AuthController::class, function ($c) {
    return new AuthController($c->get(RegisterUser::class));
});

- **AuthCOntroller es el  #Adaptadores de la API (Capa de infraestructura)**
- Recibe RegisterUser Como depedencia que necesita ejecutar el caso de uso cuando alguien se registre
 - Cuando el usuario haga un POST /register , Slim llamara al controlador que a su vez usara RegisterUser

# Como funciona un flujo (Registro por ejemplo)
#FlujoDeArquitecturaHexagonal
### El usuario hace una peticion
	POST /register
		{
		  "email": "test@example.com",
		  "password": "123456"
		}
#### Slim llama a *AuthController::register()*

	public function register(Request $request, Response $response): Response {
	    $data = (array)$request->getParsedBody();
	    try {
	        $this->registerUser->execute($data['email'], $data['password']);
	        $response->getBody()->write(json_encode(["message" => "Usuario registrado con éxito"]));
	        return $response->withHeader('Content-Type', 'application/json')->withStatus(201);
	    } catch (\Exception $e) {
	        $response->getBody()->write(json_encode(["error" => $e->getMessage()]));
	        return $response->withHeader('Content-Type', 'application/json')->withStatus(400);
	    }
	}
- Recibe los datos email y password
- Llama a *$this->registerUser->execute()* **Este ejecuta el caso de uso**
#### El caso de uso (RegisterUser ) maneja la logica de negocio

		public function execute(string $email, string $password): void {
		    if ($this->userRepository->findByEmail($email)) {
		        throw new \Exception("El usuario ya existe");
		    }
			    $user = new User(Uuid::uuid4()->toString(), $email, $password);
			    $this->userRepository->save($user);
		}
- **Primero verifica si el usuario ya existe**
- Se crea un nuevo objeto **User** con un ID unico\
- Guarda el usuario en la base de datos llamando a 
	**$this->userRepository->save($user)**

#### El repositorio (UserRepositoryImpl) guarda el usuario
	public function save(User $user): void {
		    $stmt = $this->db->prepare("INSERT INTO users (id, email, password) VALUES (:id, :email, :password)");
		    $stmt->execute([
		        'id' => $user->getId(),
		        'email' => $user->getEmail(),
		        'password' => password_hash($user->getPassword(), PASSWORD_DEFAULT)
    ]);
}
