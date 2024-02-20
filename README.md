# Proyecto API RESTful de Gestión de Usuarios
Esta aplicación implementa una API RESTful para la gestión de usuarios. La API proporciona endpoints para el registro, modificación, listado de usuarios y generación de tokens de acceso al iniciar sesion o registrarse para realizar operaciones definidas.

# Herramientas
-Java 8 o superior
H2
Maven
Spring
Git
Lombok
JWT

# Instalacion: 
Siga estos pasos para instalar y ejecutar el proyecto:

Clonar el repositorio:git clone https://github.com/irojascorsico/spring-boot-jwt-authenticadion.git
Navegue al directorio del proyecto:cd your-repo
Construya el proyecto usando Maven::mvn clean install
Ejecute el proyecto:mvn spring-boot:run
Pruebe API Rest usando Postman u otra aplicación en http://localhost:8080.

# Rutas:
http://localhost:3001/h2-ui -----Base de datos H2
POST localhost:3001/users/registro
POST localhost:3001/users/login
GET localhost:3001/auth/listar
PUT localhost:3001/auth/modificar/{username}



# Endpoints
Registrar Usuario

URL: localhost:3001/users/registro
Método HTTP: POST
Descripción: Registra un nuevo usuario en el sistema y retorna token de acceso/operacion.
Cuerpo de la Solicitud (JSON):
{
    "name": "Pedro Pérez",
    "username": "rosico@perez.nkK",
    "password": "Perez2023@",
    "phones": [
        {
            "number": "5554443",
            "citycode": "3",
            "countrycode": "57"
        }
    ]
}
Consideraciones:
El formato del correo debe ser el correcto :example@exam.com
El formato de la contraseña debe contener como minimo 8 caracteres, una mayuscula, una minuscula y un numero :testeo123S
Si el username ingresado se encuentra en la base de datos vinculado a un usuario,no se permitira el registro
Respuesta Exitosa (HTTP 201):
Retorna datos especificos del usuario recién creado con un token de acceso.
Respuesta Fallo (HTTP 400): 
Mensaje de error con formato 
{
     "mensaje": "El formato del correo electrónico no es válido"
}
Respuesta Fallo (HTTP 409): 
Mensaje de error con formato 
{
  "mensaje": "El correo rosico@perez.com ya ha sido registrado para otro usuario"
}


Login Usuario

URL: localhost:3001/users/login
Método HTTP: POST
Descripción: Valida datos de un usuario registrado en el sistema y retorna token de acceso/operacion.
Cuerpo de la Solicitud (JSON):
{
   {
    "username": "pedro@perez.nekkK",
    "password": "Perez2023@"
   }
}
 
Respuesta Exitosa (HTTP 200):
Retorna token de acceso con formato :
{
    "token": "eyJhbGciOiJIUzI1NiJ9"
}
Respuesta Fallo (HTTP 400): 
Mensaje de error con formato 
{
    "mensaje": "El usuario no existe"
}
Respuesta Fallo (HTTP 500): 
Mensaje de error con formato 
{
     "mensaje": "Error al generar el token: Bad credentials"
}


Modificar Usuario
URL: localhost:3001/auth/modificar/{username}
Método HTTP: PUT
Authorization: Bearer Token
Descripción: Modifica los datos de un usuario existente.
Parámetro de Ruta: username - El correo electrónico del usuario a modificar.
Cuerpo de la Solicitud (JSON):

{
"name": "rosita",
"username": "rosita@rodriguez.com",
"password": "justino123@S",
"phones": [
        {
            "number": 88888,
            "citycode": "3",
            "countrycode": "57"
        },
         {
            "number": 666,
            "citycode": "3",
            "countrycode": "55"
        }
    ]
}

Consideraciones:
El formato del correo debe ser el correcto :example@exam.com
El formato de la contraseña debe contener como minimo 8 caracteres, una mayuscula, una minuscula y un numero :testeo123S
En caso, la solicitud no tenga atributos con valor, persistiran los datos de la ultima actualizacio nen la base de datos
Si el username ingresado se encuentra en la base de datos vinculado a un usuario,no se permitira el registro
Se valida el bearer token, en caso de no proporcionarlo la solicitud sera marcada como forbidden

Respuesta Exitosa (HTTP 200):
Retorna el usuario modificado.
 Respuesta Fallo (HTTP 400): 
Mensaje de error con formato 
{
     "mensaje": "El formato del correo electrónico no es válido"
}
{
    "mensaje": "El usuario no existe"
}
Respuesta Fallo (HTTP 409): 
Mensaje de error con formato 
{
  "mensaje": "El correo rosico@perez.com ya ha sido registrado para otro usuario"
}
Respuesta Fallo (HTTP 403):
Bearer Token no autorizado o no proporcionado



Listado de Usuarios
URL: localhost:3001/auth/listar
Método HTTP: GET
Authorization: Bearer Token
Descripción: Obtiene la lista de todos los usuarios registrados en el sistema.
Respuesta Exitosa (HTTP 200):
Retorna una lista de usuarios.
Respuesta Fallo (HTTP 403):
Bearer Token no autorizado o no proporcionado













