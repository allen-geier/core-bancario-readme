# TEGRITY CORE 2

  - [QUOTATION](#quotation)
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
- [Quotations](#quotations)  
- [Consolidated](#consolidated)
- [No Core](#no-core)  


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
```json
{
    "first_name":"{{$randomFirstName}}",
    "middel_name": "{{$randomFirstName}}",
    "last_name": "{{$randomLastName}}"
}
```

##### Response
```json
{
    "uuid": {{uuid}}
}
```


### <ins>Edit Client:</ins>  
### PATCH /api/clients/{uuid}

Permite modificar los campos del objeto Client que uno quiera.

#### Ejemplo de Request y Response

##### Request
```json
{
    "middle_name": "Morty"
}
```

##### Response
```json
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
```


### <ins>List Clients:</ins>  
### GET /api/clients/query

Permite listar todos los clientes.

#### Ejemplo de Request y Response

##### Response
```json
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
]
```

Tambien permite buscar por query params, los posibles campos son: external_id, first_name, last_name
Path: /api/clients/query?last_name=Gian_Marco

### <ins>Delete Client:</ins>  
### DELETE /api/clients/{uuid}

Permite borrar un cliente. (por ahora parece que el metodo no esta disponible) (es un soft delete)

#### Ejemplo de Request y Response

##### Response
```json
{
    "detail": "Method \"DELETE\" not allowed."
}
```


### <ins>Find Client by Id</ins>  
### GET /api/clients/{uuid}

Permite buscar un cliente por ID.

#### Ejemplo de Request y Response

##### Response
```json
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
```

También permite buscar por query params, por ej:
/api/clients/fb0ae303-89a0-4b79-88c9-8885e9b58418?details=accounts,loans


### <ins>Define Client Identifier:</ins>  
### POST /api/clients/identifier

Permite definir un tipo de identificador, ej DNI.

#### Ejemplo de Request y Response

##### Request
```json
{
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",
    "identifier_type":"CUIT",
    "identifier_key":"39371777",
    "description": "",
    "metadata": {"hola":"universo"}
}
```


##### Response   
```json
{
    "uuid": "cf4022ee-9d7a-4690-96a6-8b7af040b770"
}
```


## Accounts  
  - [Create Client](#create-client)  
  - [Find Account by Id](#find-account-by-id)  
  - [Find all Accounts](#find-all-accounts)  


### <ins>Create Account</ins>  
### POST /api/accounts  

Permite crear una cuenta para un cliente pasando un uuid en el body.  

#### Ejemplo de Request y Response  

##### Request  
```json
{
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",
    "currency": "MXN"
}
```

##### Response  
```json
{
    "uuid": "203f5906-c18f-453d-9e2d-e2dcf0400a8b"
}
```


### <ins>Find Account by Id</ins>  
### GET /api/accounts/{account_id}  

Permite obtener los datos de una cuenta buscando por account_id.  

#### Ejemplo de Request y Response  

##### Response  
```json
{
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",
    "description": null,
    "metadata": null,
    "account_type": "COLLECTING",
    "account_status": "ACTIVE",
    "amount": 0.0,
    "currency": "MXN"
}
```


### <ins>Find all Accounts</ins>  
### GET /api/accounts  

Permite obtener una lista de todas las cuentas.  

#### Ejemplo de Request y Response  

##### Response  
```json
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
```

Tambien permite buscar por query params, los posibles campos son: uuid, account_type, account_status, client, client__external_id.  
Path: /api/accounts/query?client__external_id=gustavito&client=b287dab4-7571-4a25-a7fc-52ec0bfc7435  


## Quotations  
  - [Quote](#quote)  
  - [Fix Quotation](#fix-quotation)  
  - [Obtain Quotation](#obtain-quotation)  
    

### <ins>Quote:</ins>  
### POST /api/loan-quotation  

Permite crear una cotizacion, con un monto, cuotas e impuestos.

#### Ejemplo de Request y Response

##### Request
```json
{
    "amount": 100000,
    "installments": 3,
    "tna":123,
    "tax": 21.0
}
```

##### Response  
```json
{
    "principal": 100000.0,
    "plan": [
        {
            "installment": 1,
            "interes": 10250.0,
            "tax": 2152.5,
            "amortization": 29520.67,
            "capital": 70479.33,
            "payment": 41923.17,
            "fee": 0.0
        },
        {
            "installment": 2,
            "interes": 7224.13,
            "tax": 1517.07,
            "amortization": 33181.97,
            "capital": 37297.36,
            "payment": 41923.17,
            "fee": 0.0
        },
        {
            "installment": 3,
            "interes": 3822.98,
            "tax": 802.83,
            "amortization": 37297.36,
            "capital": 0.0,
            "payment": 41923.17,
            "fee": 0.0
        }
    ],
    "plan_uuid": "c2cad34d-2b48-48ea-9c46-0bf2e45cf423"
}
```

API en construccion.
### <ins>Fix Quotation:</ins>  
### POST /api/loan-fixed-quotation  

TODO  

#### Ejemplo de Request y Response  

##### Request  
```json
{
    "amount": 100.0,
    "expirations" :[{
        "date": "2023-12-22",
        "amount": 100,
        "fee": 50
    }
    ],
    "arreas_tolerance": 0,
    "arreas_interes": 10,
    "arreas_tax": 21
}
```

##### Response  
```json
[
    {
        "date": "2023-12-22",
        "amount": 100,
        "fee": 50
    }
]
```


### <ins>Obtain Quotation:</ins>  
### GET /api//loan-quotation/{quotation_id}  

Permite obtener una cotizacion de prestamo, con sus respectivas cuotas e intereses, por id.  

#### Ejemplo de Request y Response  

##### Response  
```json
{
    "amount": 100000.0,
    "installments": 3,
    "tna": 123.0,
    "tax": 21.0,
    "days_in_year": 360,
    "days_in_month": 30,
    "expired": "2023-09-07T07:32:33.417417Z",
    "plan": {
        "plan": [
            {
                "fee": 0.0,
                "tax": 2152.5,
                "capital": 70479.33,
                "interes": 10250.0,
                "payment": 41923.17,
                "installment": 1,
                "amortization": 29520.67
            },
            {
                "fee": 0.0,
                "tax": 1517.07,
                "capital": 37297.36,
                "interes": 7224.13,
                "payment": 41923.17,
                "installment": 2,
                "amortization": 33181.97
            },
            {
                "fee": 0.0,
                "tax": 802.83,
                "capital": 0.0,
                "interes": 3822.98,
                "payment": 41923.17,
                "installment": 3,
                "amortization": 37297.36
            }
        ],
        "principal": 100000.0
    }
}
```


## Consolidated  
  - [Create Loan](#create-loan)  
    

### <ins>Create Loan:</ins>  
### POST /api/loan?COLLECTING=create  

Permite crear un nuevo prestamo, pasandole en el body un client_id y un quotation_id.  

#### Ejemplo de Request y Response  

##### Request  
```json
{
    "quotation": "c2cad34d-2b48-48ea-9c46-0bf2e45cf423",
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823"
}
```

##### Response  
```json
{
    "uuid": "84c15350-3052-4553-bfd0-3c20fa0f60a7",
    "plan": [
        {
            "fee": 0.0,
            "tax": 2152.5,
            "capital": 70479.33,
            "interes": 10250.0,
            "payment": 41923.17,
            "installment": 1,
            "amortization": 29520.67
        },
        {
            "fee": 0.0,
            "tax": 1517.07,
            "capital": 37297.36,
            "interes": 7224.13,
            "payment": 41923.17,
            "installment": 2,
            "amortization": 33181.97
        },
        {
            "fee": 0.0,
            "tax": 802.83,
            "capital": 0.0,
            "interes": 3822.98,
            "payment": 41923.17,
            "installment": 3,
            "amortization": 37297.36
        }
    ],
    "description": null,
    "created_at": "2023-09-04T20:04:16.477614Z",
    "update_at": "2023-09-04T20:04:16.477644Z",
    "metadata": null,
    "external_id": null,
    "principal_amount": 100000.0,
    "state": "OPEN",
    "client": "9d217374-b4f4-4acb-9f9d-98df0a3a0823",
    "product": null,
    "quotation": "c2cad34d-2b48-48ea-9c46-0bf2e45cf423",
    "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b"
}
```


## No Core  
  - [Get Identifiers](#get-identifiers)  
  - [Create Identifier](#create-identifier)  
  - [Get States](#get-states)  
  - [Get Currencies](#get-currencies)  
  - [Get Countries](#get-countries)  


### <ins>Get Identifiers:</ins>  
### GET /api/identifier  

Permite obtener todos los identifiers creados (ej: DNI, CUIT, etc).  

#### Ejemplo de Request y Response  

##### Response  
```json
[
    {
        "uuid": "6895f8e6-0d21-4a42-a1b9-2979b44b5cac",
        "name": "CURP",
        "created_at": "2023-08-21T18:11:03.357579Z",
        "update_at": "2023-08-21T18:11:03.357612Z",
        "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b"
    },
    {
        "uuid": "f48a8e12-29b6-4de1-a1e5-77ad183cb0d2",
        "name": "DNI",
        "created_at": "2023-09-04T16:46:35.643582Z",
        "update_at": "2023-09-04T16:46:35.643617Z",
        "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b"
    }
]
```


### <ins>Create Identifiers:</ins>  
### POST /api/identifier  

Permite obtener todos los identifiers creados (ej: DNI, CUIT, etc).  

#### Ejemplo de Request y Response  

##### Request  
```json
{
        "name": "CUIL"
}
```

#### Response  
```json
{
    "uuid": "cc1a68f6-0a9a-4c0b-88c0-ac3a6e89e6a8",
    "name": "CUIL",
    "created_at": "2023-09-04T20:22:08.796444Z",
    "update_at": "2023-09-04T20:22:08.796466Z",
    "tenant": "7365a80b-b1fe-4560-a044-699e33f9554b"
}
```


### <ins>Get States:</ins>  
### POST /api/states  

Permite obtener todos un listado con todos los estados.  

#### Ejemplo de Request y Response  

##### Response  
```json
[
    {
        "uuid": "0d1aaec0-f8ab-4233-9117-eec063920395",
        "name": "Aguascalientes",
        "created_at": "2023-08-15T16:54:42.633938Z",
        "update_at": "2023-08-15T16:57:09.837949Z",
        "metadata": null,
        "country": "MEX"
    },
    {
        "uuid": "81d7b119-907c-4754-81a6-dfde54230702",
        "name": "Baja California",
        "created_at": "2023-08-15T16:57:49.460312Z",
        "update_at": "2023-08-21T16:39:35.410997Z",
        "metadata": null,
        "country": "MEX"
    },
    etc.  
]
```

El metodo tambien admite buscar por query param, por country.  
Path: /api/states?country=MX  


### <ins>Get Currencies:</ins>  
### GET /api/currencies  

Permite obtener todas las monedas ej: MXN, ARS, USD, EUR, etc.  

#### Ejemplo de Request y Response  

##### Response  
```json
[
    {
        "iso4217": "MXN",
        "name": "Peso Mexicano",
        "description": "",
        "metadata": null,
        "created_at": "2023-08-21T18:41:21.983789Z",
        "update_at": "2023-08-21T18:41:21.983804Z",
        "digits_after_decimals": 2
    }
]
```


### <ins>Get Countries:</ins>  
### GET /api/countries  

Permite obtener todas los paises ej: MEX, ARG, etc.  

#### Ejemplo de Request y Response  

##### Response  
```json
[
    {
        "iso3": "MEX",
        "iso2": "MX",
        "name": "Mexico",
        "description": "",
        "metadata": null,
        "created_at": "2023-08-15T16:54:24.002248Z",
        "update_at": "2023-08-15T16:54:24.002264Z"
    }
]
```
