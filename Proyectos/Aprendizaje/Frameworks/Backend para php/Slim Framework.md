#Slim

# Uso de CORS en Slimp

	Ya que php nativo ya no existe despues de colocar un framework de backend, en este caso slim se apodera de index.php, eso significa que para inicializar las rutas y contenedores primero uno debe dar permisos al backend normalmente se debe dar permisos solo al puerto que es el entrante 

	//Ya que estoy usando el framework slim debo primero definir el cors desde aqui

		$app->add(function ($request , $handler ){
		
		$response = $handler->handle($request);
		
		if($request->getMethod() === "options"){
		
		$response = new \Slim\Psr7\Response();
		
		}
		
		  
		
		return $response
		
		->withHeader("Access-Control-Allow-Origin", "*")
		
		->withHeader("Access-Control-Allow-Headers", "Content-Type, Authorization")
		
		->withHeader("Access-Control-Allow-Methods", "GET, POST, PUT , DELETE , OPTIONS");
		
		});
	Esta es una forma de activar los cors para aceptacion de otros puertos