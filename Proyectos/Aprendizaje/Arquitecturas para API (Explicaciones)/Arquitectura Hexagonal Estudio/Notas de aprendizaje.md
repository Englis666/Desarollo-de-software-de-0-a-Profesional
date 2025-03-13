#PHP8-4 
En la [[Arquitectura Recomendada para proyectos a base de estudios]] encontre que el controlador ya no tiene carpeta predefinida, se mantiene el mismo nombramiento un ejemplo para tareas seria "TaskController" y digamos que tambien en la infrastructure tambien funciona el repositorio "TaskRepository".

# Rutas Por Slim #Slim 
	La sintaxis de slim es sencilla se usa la variable 
	$app para definir las rutas y bueno, su funcionalidad con get es:
	
	$app->get('/task', function ($request, $response, $arg) use ($controllers)){
		return $response->withJson($controllers['task']->getAllTask())
	});
	
		Y con post seria:
		
	$app->post('/tasks', function ($request, $response, $args) use ($controllers) { $data = $request->getParsedBody(); return $response->withJson($controllers['task']->createTask($data)); });

	y para iniciar la aplicacion siempre debo usar 
	$app->run(); al final del archivo rutas


# Como esto ayuda a la seguridad? #seguridad
#### Proteccion contra ataques comunes
- Slim maneja automaticamente CSRF CORS y las validaciones si se configuran
- Mejor gestion de entradas de usuario con getParsedBody()
##### Autentificacion y autorizacion
- Se integra JWT o Auth2
- Ya de por si agregar un middleware para proteger las rutas $app
##### Mejor manejo de los errores
- Slim ayuda con las respuestas JSON en caso de errores
-  Se pueden personalizar los codigos HTTP (400, 401, 500, 404)