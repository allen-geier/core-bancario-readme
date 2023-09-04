# TEGRITY CORE 2

- [CORE BANCARIO](#core-bancario)  
  - [Despliegue](#despliegue)  
  - [Metodos expuestos](#metodos-expuestos)

## Despliegue  

**Título del Producto:** Tegrity Core 2  
**Nombre:** tegrity-core-2  
**Version:** 1.0.0  
**Security:** apikey  
**URL:** https://tegrity-core.onrender.com  

## Metodos expuestos  

### External API  
- [Clients](#clients)
- [Accounts](#accounts)

## Clients
  - [Create Client](#create-client)  
  - [Edit Client](#edit-client)  
  - [List Clients](#list-clients)  
  - [Delete Client](#delete-client)  
  - [Find Client by Id](#find-client-by-id)  
  - [Define Client Identifier](#define-client-identifier)  

### <ins>Create Client:</ins>  
### POST /api/clients

Permite crear un cliente.

#### Ejemplo de Request y Response

##### Request
{  
    "first_name":"{{$randomFirstName}}",  
    "middel_name": "{{$randomFirstName}}",  
    "last_name": "{{$randomLastName}}"  
}  

##### Response
{  
    "uuid": {{uuid}}  
}  


### <ins>Edit Client:</ins>  
### PATCH /api/clients/{uuid}

Permite modificar los campos del objeto Client que uno quiera.

#### Ejemplo de Request y Response

##### Request
{  
    "middle_name": "Morty"  
}  

##### Response
{  
    "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b",  
    "first_name": "Thomas",  
    "last_name": "Greenfelder",  
    "middle_name": "Morty",  
    "external_id": null,  
    "active": true,  
    "activation_date": null,  
    "metadata": null,  
    "status": "NEW"  
}  


### <ins>List Clients:</ins>  
### GET /api/clients/query

Permite listar todos los clientes.

#### Ejemplo de Request y Response

##### Response
[  
    {  
        "uuid": "79613581-d0e8-4b39-b7bf-0420a5186578",  
        "first_name": "pollo",  
        "last_name": "loco",  
        "middle_name": null,  
        "external_id": null,  
        "created_at": "2023-08-02T15:37:13.112332Z",  
        "update_at": "2023-08-02T15:37:13.112367Z",  
        "active": false,  
        "activation_date": null,  
        "metadata": null,  
        "status": "NEW"  
    },  
    {  
        "uuid": "cf27603b-9f11-446c-9be2-6705f218b5bb",  
        "first_name": "Donna",  
        "last_name": "Nader",  
        "middle_name": null,  
        "external_id": "123",  
        "created_at": "2023-08-21T18:39:24.043158Z",  
        "update_at": "2023-08-21T18:39:24.043191Z",  
        "active": false,  
        "activation_date": null,  
        "metadata": null,  
        "status": "NEW"  
    }  
[  

Tambien permite buscar por query params, los posibles campos son: external_id, first_name, last_name
Path: /api/clients/query?last_name=Gian_Marco

### <ins>Delete Client:</ins>  
### DELETE /api/clients/{uuid}

Permite borrar un cliente. (por ahora parece que el metodo no esta disponible) (es un soft delete)

#### Ejemplo de Request y Response

##### Response
{  
    "detail": "Method \"DELETE\" not allowed."  
}  


### <ins>Find Client by Id</ins>  
### GET /api/clients/{uuid}

Permite buscar un cliente por ID.

#### Ejemplo de Request y Response

##### Response
{  
    "first_name": "Thomas",  
    "last_name": "Greenfelder",  
    "middle_name": null,  
    "external_id": null,  
    "active": true,  
    "activation_date": null,  
    "metadata": null,  
    "status": "NEW"  
}  


### <ins>Define Client Identifier:</ins>  
### POST /api/clients/identifier

Permite definir un tipo de identificador, ej DNI.

#### Ejemplo de Request y Response

##### Request
{  
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",  
    "identifier_type":"CUIT",  
    "identifier_key":"39371777",  
    "description": "",  
    "metadata": {"hola":"universo"}  
}  

##### Response (no consegui un 200OK, solo este 404)  
{  
    "uuid": "cf4022ee-9d7a-4690-96a6-8b7af040b770"  
}  


## Accounts  
  - [Create Client](#create-client)  
  - [Find Account by Id](#find-account-by-id)  
  - [Find all Accounts](#find-all-accounts)  


### <ins>Create Account</ins>  
### POST /api/accounts  

Permite crear una cuenta para un cliente pasando un uuid en el body.  

#### Ejemplo de Request y Response  

##### Request  
{  
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",  
    "currency": "MXN"  
}  

##### Response  
{  
    "uuid": "203f5906-c18f-453d-9e2d-e2dcf0400a8b"  
}  


### <ins>Find Account by Id</ins>  
### GET /api/accounts/{account_id}  

Permite obtener los datos de una cuenta buscando por account_id.  

#### Ejemplo de Request y Response  

##### Response  
{  
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",  
    "description": null,  
    "metadata": null,  
    "account_type": "COLLECTING",  
    "account_status": "ACTIVE",  
    "amount": 0.0,  
    "currency": "MXN"  
}  


### <ins>Find all Accounts</ins>  
### GET /api/accounts  

Permite obtener una lista de todas las cuentas.  

#### Ejemplo de Request y Response  

##### Response  
[  
    {  
        "uuid": "64765f25-d236-43e8-8850-97b2b1a91271",  
        "description": null,  
        "metadata": null,  
        "created_at": "2023-08-21T19:24:33.680733Z",  
        "update_at": "2023-08-21T19:24:33.680764Z",  
        "account_type": "REGULAR",  
        "account_status": "ACTIVE",  
        "amount": 0.0,  
        "client": "e052d2bf-040a-4051-ac26-012de7648d88",  
        "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b",  
        "currency": "MXN"  
    },  
    {  
        "uuid": "12a88168-dfc9-4380-a0b3-56cde20786c8",  
        "description": null,  
        "metadata": null,  
        "created_at": "2023-08-21T19:47:36.143013Z",  
        "update_at": "2023-08-21T19:47:36.143034Z",  
        "account_type": "REGULAR",  
        "account_status": "ACTIVE",  
        "amount": 0.0,  
        "client": "cf27603b-9f11-446c-9be2-6705f218b5bb",  
        "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b",  
        "currency": "MXN"  
    }  
]  



