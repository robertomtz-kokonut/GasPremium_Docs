---
title: Gas Premium API

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript: Request Body
  - csharp: Success Response
  - java: Error Response

toc_footers:
  - <a href='http://kokonutstudio.com/'>Kokonut Studio</a>

search: true
---

# Gas Premium API Reference
Link al código fuente: [GasPremium_Backend](https://github.com/KokonutStudioRepository/GasPremium_Backend).

## URL
Ambiente        | Value
----------------|----------------------------------------
Pruebas Kokonut | https://api.gaspremium.com.mx/
Producción      | https://api-s.gaspremium.com.mx/

## Keys
Descripción                    | Value
-------------------------------|----------------------------------------
Conekta Public Key Development | key_OEdDTWP4mMYAnrmivuiSTKA
Conekta Public Key Production  | key_cb4ycoccpDb8oL2nHWtZoGw
Google API Key Android         | AIzaSyDZX-0g3lRHLPAvwFJscXN-UA5q99uAuZ4
Google API Key iOS             | NO DISPONIBLE AÚN

# User
## Registro de usuarios
> Registro de usuarios:

```javascript
// Registro con correo electrónico y contraseña
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "email": "developer@kokonutstudio.com",
    "password": "123qwe",
    "phone": "5522222222",
    "firebase_id": "esd8669JSL...",
    "device": 2
}
// Registro con Token de Facebook
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "email": "developer@kokonutstudio.com",
    "fbuid": "eyJ0eXAiOi...cRgHhBjwU",
    "firebase_id": "esd8669JSL...",
    "device": 2
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
{
  "success": 0,
  "message": "Hace falta enviar información.",
  "data": null
}
{
  "success": 0,
  "message": "Correo electrónico previamente registrado.",
  "data": null
}
{
  "success": 0,
  "message": "Usuario Facebook registrado previamente.",
  "data": null
}
```

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------
POST          | register      | {{url}}/api/register

### Headers
No requerido.

### Body
Key         | Descripción                                      | Type   | Mandatory
------------|--------------------------------------------------|--------|----------------------------
name        | Nombre del usuario                               | String | Siempre
last_name   | Apellidos del usuario                            | String | Siempre
username    | Correo electrónico del usuario                   | String | Siempre
password    | Contraseña de acceso del usuario                 | String | Solo si es registro con correo y contraseña
phone       | Teléfono del usuario                             | String | Opcional
fbuid       | Token de acceso Facebook                         | String | Solo si es registro con Facebook
firebase_id | Token de Firebase Messaging                      | String | Opcional
device      | Indica el dispositivo que dió de alta al usuario | String | Siempre



## Inicio de sesión
> Inicio de sesión:

```javascript
// Inicio de sesión con correo electrónico y contraseña
{
    "username": "developer@kokonutstudio.com",
    "password": "123qwe",
    "firebase_id": "esd8669JSL..."
}
// Inicio de sesión con Facebook Token
{
    "fbuid": "0000000000...123456789",
    "firebase_id": "esd8669JSL..."
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
{
  "success": 0,
  "message": "Hubo un error al autenticar el usuario.",
  "data": null
}
{
  "success": 0,
  "message": "Usuario o contraseña no valida.",
  "data": null
}
{
  "success": 0,
  "message": "El usuario Facebook no existe.",
  "data": null
}
{
    "success": 0,
    "message": "Es necesario activar tu cuenta.",
    "data": null
}
```

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|---------------------
POST          | login         | {{url}}/api/login

### Headers
No requerido.

### Body
Key         | Descripción                      | Type   | Obligación de envío
------------|----------------------------------|--------|---------------------------------------------
username    | Correo electrónico del usuario   | String | Solo si es login con correo y contraseña
password    | Contraseña de acceso del usuario | String | Solo si es login con correo y contraseña
firebase_id | Token de Firebase Messaging      | String | Opcional
fbuid       | Token de acceso Facebook         | String | Solo si es login con Facebook



## Obtener perfil
> Obtener perfil:

```javascript
// No requerido
```
```csharp
{
    "success": 1,
    "message": null,
    "data": [
        {
            "id": 14,
            "name": "Roberto",
            "phone": "5522121212",
            "last_name": "Kokonut Studio",
            "email": "roberto@kokonutstudio.com",
            "fbuid": null,
            "address": null,
            "image": "",
            "firebase_id": "eG1o9lBrw5M...",
            "conekta_id": null,
            "user_type_id": 2,
            "user_status_id": 1,
            "password_token": "CRzPvpO3ZDCUjwAQZOiGxISHhI98Lr",
            "created_at": "2019-09-04 12:14:56",
            "updated_at": "2019-09-17 18:27:17"
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

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|------------------
GET           | get profile   | {{url}}/api/profile

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.



## Actualizar perfil
> Ejemplo:

```javascript
{
    "name": "Developer",
    "last_name": "Kokonut Studio",
    "phone": "5522222222",
    "password": "123qwe1"
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
{
  "success": 0,
  "message": "Unauthenticated",
  "data": []
}
```

HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
PUT           | update profile  | {{url}}/api/user/update

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Parámetros
Key         | Descripción                      | Type    | Obligación de envío
------------|----------------------------------|---------|----------------------
name        | Nombre del usuario               | String  | Opcional
last_name   | Apellidos del usuario            | String  | Opcional
phone       | Teléfono del usuario             | String  | Opcional
password    | Contraseña                       | String  | Opcional





# Métodos de Pago
## Registrar método de pago
> Registrar método de pago:

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

HTTP Request  | Name Endpoint        | Endpoint
--------------|----------------------|-------------------------------------
POST          | save method payment  | {{url}}/api/save-method-payment

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key         | Descripción                                                   | Type    | Obligación de envío
------------|---------------------------------------------------------------|---------|---------------------
token_id    | Valor obtenido de tokenizar una tarjeta con el SDK de Conekta | String  | Siempre



## Obtener métodos de pago
> Obtener métodos de pago:

```javascript
// No requerido
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
GET           | get method payment   | {{url}}/api/method-payment

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.



## Eliminar método de pago
> Eliminar método de pago:

```javascript
{
  "method_id": "src_2kahPKe67FNYTLwWx"
}
```
```csharp
{
  "success": 1,
  "message": "Método de pago eliminado correctamente.",
  "data": null
}
```
```java
{
  "success": 0,
  "message": "El método de pago no existe.",
  "data": null
}
```

HTTP Request  | Name Endpoint          | Endpoint
--------------|------------------------|---------------
POST          | delete method payment  | {{url}}/delete-method-payment

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key         | Descripción                                            | Type    | Obligación de envío
------------|--------------------------------------------------------|---------|---------------------
method_id   | Source id asociado a la tarjeta previamente registrada | String  | Siempre



## Obtener el historial de pagos
> Obtener el historial de pagos:

```javascript
// No requerido
```
```csharp
{
    "success": 1,
    "message": null,
    "data": [
        {
            "id": 47,
            "amount": "414.48",
            "conekta_order_id": "ord_2mJdD5dtPnEajUTUX",
            "payment_method": "saved",
            "payed": 0,
            "payment_reference": null,
            "last_digits": "4242",
            "folio": "RrpCRKXQhCW7NKu9DFOugp4CuDM8rWraEZc",
            "payment_source": "src_2mGYpJ8hfwP2Mqgt2",
            "payment_status_id": 1,
            "created_at": "2019-09-10 20:51:51",
            "updated_at": "2019-09-10 20:51:51",
            "description": "paid",
            "order_id": 121
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

HTTP Request  | Name Endpoint        | Endpoint
--------------|----------------------|---------------
GET           | get history payments | {{url}}/api/get-payments

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.





# Visita
## Obtener fechas disponibles
> Obtener fechas disponibles:

```javascript
// No requerido.
```
```csharp
{
    "success": 1,
    "message": null,
    "data": [
        {
            "date": "2019-09-26",
            "hours": [
                "13:00:00",
                "14:00:00",
                "15:00:00"
            ]
        },
        {
            "date": "2019-09-27",
            "hours": [
                "9:00:00",
                "10:00:00",
                "11:00:00",
                "12:00:00",
                "13:00:00",
                "14:00:00",
                "15:00:00"
            ]
        }
    ]
}
```
```java
// Sin ejemplo replicable
```

HTTP Request  | Name Endpoint        | Endpoint
--------------|----------------------|---------------
GET           | get available dates  | {{url}}/api/get-dates

### Headers
No requerido.

### Body
No requerido.



## Obtener precio por litro
> Obtener precio por litro:

```javascript
// No requerido
```
```csharp
{
    "success": 1,
    "message": null,
    "data": {
        "price": 9.87
    }
}
```
```java
// Sin ejemplo replicable
```

HTTP Request  | Name Endpoint   | Endpoint
--------------|-----------------|-------------------
GET           | get price       | {{url}}/get-price

### Headers 
No requerido.

### Body
No requerido.



## Validar ubicación
> Validar ubicación:

```javascript
{
    "latitude": 19.38823,
    "longitude": -99.1632896
}
```
```csharp
{
  "status": 200,
  "latitude": 19.4357068,
  "longitude": -99.131757,
  "valid": true,
  "msg": "Location is inside any polygon",
  "polygons_ids": {
    "1": "50b5000e8c414e528d4a51c9b1ea611b"
  }
}
{
  "status": 200,
  "latitude": 19.4357068,
  "longitude": -99.131757,
  "valid": false,
  "msg": "Location is not inside any polygon",
  "polygons_ids": []
}
```
```java
// Sin ejemplo replicable
```

HTTP Request  | Name Endpoint   | Endpoint
--------------|-----------------|--------------------------------------------------------
POST          | validate area   | https://validatearea.kokonutstudio.com/api/v1/user/1

### Headers 
No requerido.

### Body
Key         | Descripción                        | Type    | Obligación de envío
------------|------------------------------------|---------|---------------------
latitude    | Latitud de la ubicación a validar  | Double  | Siempre
longitude   | Longitud de la ubicación a validar | Double  | Siempre



## Solicitar visita
> Solicitar visita:

```javascript
// Pago en efectivo
{
  "address": "Centro Histórico de la Cdad. de México, Centro, Ciudad de México, CDMX, México",
  "address_detail": "Descripción de ubicación",
  "cash_amount": 500.0,
  "date": "2019-09-26 13:00:00",
  "latitude": "19.4357068",
  "longitude": "-99.131757",
  "liters": "50.0",
  "payment_method": "cash"
}
// Pago con tarjeta a contra-entrega
{
  "address": "Centro Histórico de la Cdad. de México, Centro, Ciudad de México, CDMX, México",
  "date": "2019-09-26 14:00:00",
  "latitude": "19.4357068",
  "longitude": "-99.131757",
  "liters": "50.0",
  "payment_method":"delivery"
  }
// Pago con tarjeta al momento
{
  "address": "Centro Histórico de la Cdad. de México, Centro, Ciudad de México, CDMX, México",
  "date": "2019-09-26 15:00:00",
  "latitude": "19.4357068",
  "longitude": "-99.131757",
  "liters": "50.0",
  "payment_method": "saved",
  "payment_source_id": "src_2mGYpJ8hfwP2Mqgt2"
}
```
```csharp
// Visita programada correctamente
{
    "success": 1,
    "message": null,
    "data": {
        "folio": "ua1Ckipg1Y1MclCTf8MSrGopX8Gy7uTCUrP"
    }
}
// Visita programada y pagada correctamente
{
  "success": 1,
  "message": null,
  "data": {
    "status": "Pagado",
    "auth_code": "683919",
    "conekta_order_id": "ord_2mPQsYvPt3iVY14wf",
    "payment_reference": null,
    "folio": "UfWSX7tZAnXefE5oxzD8PmLjv1b9b76b4C9"
  }
}
```
```java
// Source id incorrecto
{
  "success": 0,
  "message": "La tarjeta no esta asociada al cliente.",
  "data": null
}
```

HTTP Request  | Name Endpoint  | Endpoint
--------------|----------------|---------------
POST          | request gas    | {{url}}/request-gasoline

### Headers
Key          | Value 
-------------|----------------------------------
Autorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key               | Descripción                                                                          | Type                    | Obligación de envío
------------------|--------------------------------------------------------------------------------------|-------------------------|---------
liters            | Cantidad de litros solicitados por el cliente                                        | Double                  | Siempre
date              | Fecha en la que se solicita la visita con el siguiente formato: "YYYY-MM-DD h:mm:ss" | String                  | Siempre
address           | Dirección para realizar la visita                                                    | String                  | Siempre
address_detail    | Descripción extra para la dirección                                                  | String                  | Opcional
latitude          | Latitud en la que se encuentra ubicada la dirección del usuario                      | Long                    | Siempre
longitude         | Longitud en la que se encuentra ubicada la dirección del usuario                     | Long                    | Siempre
payment_method    | Valor que indica con qué tipo de método de pago será realizada la petición           | saved - cash - delivery | Siempre
cash_amount       | Cantidad con la que el usuario pagará en efectivo                                    | Double                  | Solo si payment_method es "cash"
payment_source_id | Source id asociado a la tarjeta previamente registrada                               | String                  | Solo si payment_method es "saved"