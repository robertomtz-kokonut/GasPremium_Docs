---
title: Gas Premium API

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript: Request
  - csharp: Success Response
  - java: Error Response

toc_footers:
  - <a href='http://kokonutstudio.com/'>Kokonut Studio</a>

search: true
---

# Gas Premium API Reference
Link al código fuente: [GasPremium_Backend](https://github.com/KokonutStudioRepository/GasPremium_Backend).

### API BASE URL
Variable |  Value
--------------|---------
{{url}} | https://gasapi.kokonutstudio.com/api

<aside class="notice">
Si la respuesta de los servicios son llevadas a cabo satisfactoriamente se devuelve como Success <code>1</code> y si no, se devuelve <code>0</code>.
</aside>



# APP-ENPOINTS
Servicios expuestos para consumo interno de aplicaciones móviles.
# Usuarios
## Registrar un nuevo usuario
> Ejemplo:

```javascript
// Registro con correo electrónico y contraseña
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "email": "developer@kokonutstudio.com",
    "password": "123qwe",
    "phone": "5522222222"
}
// Registro con Facebook Token
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "email": "developer@kokonutstudio.com",
    "fbuid": "eyJ0eXAiOi...cRgHhBjwU"
}
```

```csharp
{
  "success": 1,
  "message": "Usuario registrado correctamente.",
  "data": null
}
```

```java
// Error por falta de parámetros
{
  "success": 0,
  "message": "Hace falta enviar información.",
  "data": null
}
// Error por duplicidad de correo electrónico
{
  "success": 0,
  "message": "Correo electrónico previamente registrado.",
  "data": null
}
// Error por duplicidad del token asociado con Facebook
{
  "success": 0,
  "message": "Usuario Facebook registrado previamente.",
  "data": null
}
```

Registra a un usuario con su correo electrónico y su contraseña ó con Token de acceso Facebook.

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------
POST          | REGISTER      | {{url}}/register

### Parámetros
Key         | Descripción                      | Type    | Obligación de envío
------------|----------------------------------|---------|---------------------------------------------
name        | Nombre del usuario               | String  | Siempre
last_name   | Apellidos del usuario            | String  | Siempre
username    | Correo electrónico del usuario   | String  | Siempre
password    | Contraseña de acceso del usuario | String  | Solo si es registro con correo y contraseña
phone       | Teléfono del usuario             | String  | Opcional
fbuid       | Token de acceso Facebook         | String  | Solo si es registro con Facebook



## Inicio de sesión
> Ejemplo:

```javascript
// Inicio de sesión con correo electrónico y contraseña
{
    "username": "developer@kokonutstudio.com",
    "password": "123qwe"
}
// Inicio de sesión con Facebook Token
{
  "fbuid": "0000000000...123456789"
}  
```

```csharp
// Inicio de sesión con correo electrónico y contraseña
{
  "token_type": "Bearer",
  "expires_in": 604800,
  "access_token": "eyJ0eXAiOi...cRgHhBjwU",
  "refresh_token": "def50a8e4...a6e90dcfe"
}
// Inicio de sesión con Facebook Token
{
  "token_type": "Bearer",
  "access_token": "eyJ0eX...juDzGI2AQz88N_tcc",
  "refresh_token": ""
}
```

```java
// Error por falta de parámetros
{
  "success": 0,
  "message": "Hubo un error al autenticar el usuario.",
  "data": null
}
// Error en la validación de credenciales por correo electrónico y contraseña
{
  "success": 0,
  "message": "Usuario o contraseña no valida.",
  "data": null
}
// Error en la validación de credenciales por Facebook Token
{
  "success": 0,
  "message": "El usuario Facebook no existe.",
  "data": null
}
```

Autentica a un usuario con su correo electrónico y su contraseña ó con Token de acceso Facebook.

### Body
HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------
POST          | LOGIN         | {{url}}/login

### Parámetros
Key         | Descripción                      | Type    | Obligación de envío
------------|----------------------------------|---------|---------------------------------------------
username    | Correo electrónico del usuario   | String  | Solo si es login con correo y contraseña
password    | Contraseña de acceso del usuario | String  | Solo si es login con correo y contraseña
fbuid       | Token de acceso Facebook         | String  | Solo si es login con Facebook



## Obtener perfil
> Ejemplo:

```javascript
/* NO BODY */
```

```csharp
{
  "success": 1,
  "message": null,
  "data": [
    {
      "id": 12,
      "name": "Jason",
      "phone": "5598054918",
      "last_name": "Garcia",
      "email": "email_1@qa.com",
      "fbuid": null,
      "address": null,
      "image": "",
      "firebase_id": null,
      "conekta_id": null,
      "user_type_id": 2,
      "created_at": "2019-05-23 15:55:17",
      "updated_at": "2019-05-23 15:55:17"
      }
      ]
}
```

```java
// Error por AccessToken incorrecto
{
  "success": 0,
  "message": "Unauthenticated",
  "data": []
}
```

Obtiene el perfil del usuario al que está asociado el Access Token 

### Body
HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|------------------
GET           | GET_PROFILE   | {{url}}/profile

### Header
Key          | Descripción                              | Type    | Obligación de envío
-------------|------------------------------------------|---------|----------------------
Autorization | AccessToken obtenido al iniciar sesión   | Bearer  | Siempre



## Actualizar perfil
> Ejemplo:

```javascript
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "phone": "5522222222"
}
```

```csharp
{
  "success": 1,
  "message": "Actualización de perfil correcta.",
  "data": null
}
```

```java
// Error por AccessToken incorrecto
{
  "success": 0,
  "message": "Unauthenticated",
  "data": []
}
```

Actualiza el perfil del usuario al que está asociado el Access Token 

### Body
HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
PUT           | UPDATE_PROFILE  | {{url}}/user/update

### Header
Key          | Descripción                              | Type    | Obligación de envío
-------------|------------------------------------------|---------|----------------------
Autorization | AccessToken obtenido al iniciar sesión   | Bearer  | Siempre

### Parámetros
Key         | Descripción                      | Type    | Obligación de envío
------------|----------------------------------|---------|---------------------------------------------
name        | Nombre del usuario               | String  | Opcional
last_name   | Apellidos del usuario            | String  | Opcional
phone       | Teléfono del usuario             | String  | Opcional






# Métodos de Pago
## Registrar un nuevo método de pago
> Ejemplo:

```javascript
{
    "token_id": "tok_test_mastercard_5100"
}
```

```csharp
{
  "success": 1,
  "message": "Metodo de pago asociado correctamente.",
  "data": null
}
```

```java
{
  "success": 0,
  "message": "Hubo un error al registar el metodo de pago del usuario.",
  "data": null
}
```

Registra y asocia a un usuario un nuevo método de pago a partir del idéntificador tokenizado de la tarjeta.

HTTP Request  | Name Endpoint        | Endpoint
--------------|----------------------|---------------
POST          | SAVE_PAYMENT_METHOD  | {{url}}/save-method-payment

### Header
Key          | Descripción                              | Type    | Obligación de envío
-------------|------------------------------------------|---------|----------------------
Autorization | AccessToken obtenido al iniciar sesión   | Bearer  | Siempre

### Parámetros
Key         | Descripción                                                   | Type    | Obligación de envío
------------|---------------------------------------------------------------|---------|---------------------
token_id    | Valor obtenido de tokenizar una tarjeta con el SDK de Conekta | String  | Siempre



## Obtener los métodos de pago de un usuario
> Ejemplo:

```javascript
/* NO BODY */
```

```csharp
// Si el usuario no tiene métodos de pago asociados
{
  "success": 1,
  "message": "Sin métodos de pago asociados.",
  "data": null
}
// Si el usuario tiene al menos un método de pago asociado
{
  "success": 1,
  "message": null,
  "data": [
    {
      "id": "src_2kgcvqDqyLfd1MdtU",
      "object": "payment_source",
      "type": "card",
      "created_at": 1558651182,
      "last4": "5100",
      "bin": "510510",
      "exp_month": "12",
      "exp_year": "19",
      "brand": "VISA",
      "name": "Jorge Lopez",
      "parent_id": "cus_2kgcvqDqyLfd1MdtR",
      "default": true
    }
  ]
} 
```

```java
{
  "success": 0,
  "message": "Unauthenticated",
  "data": []
}
```

Obtiene los métodos de pago asociados a un usuario.

HTTP Request  | Name Endpoint        | Endpoint
--------------|----------------------|---------------
GET           | GET_PAYMENT_METHODS  | {{url}}/method-payment

### Header
Key          | Descripción                              | Type    | Obligación de envío
-------------|------------------------------------------|---------|----------------------
Autorization | AccessToken obtenido al iniciar sesión   | Bearer  | Siempre