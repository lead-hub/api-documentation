# Documentação API do Leadhub

Documentação para uso dos endpoints da API para parceiros e clientes do LEADHUB

[http://www.leadhub.com.br](http://www.leadhub.com.br)

## Tecnologia

A API utiliza padrão `REST`, utiliza notação `JSON` para envio e recebimento de dados e é de fácil implementação em sua linguagem de programação preferida.

## Endpoints

Solicite ao *nosso time técnico* os endereços correspontentes à última versão da API

## Autenticação

A autenticação é feita através de token `OAUTH` e todas as chamadas serão autenticadas com esse token. O token de acesso tem uma validade de 24 horas.
Basic Authentication com as chaves criptografadas em Base64, solicite o usuário e senha do seu ambiente ao *nosso time técnico*.

### Request

**Url:** 
```
http://{endpoint}/api/token
```

**Method:**
```
POST
```

**Request Headers:**
```
Authorization = Basic {api_user:api_password pair in Base64 format}
```

**Request Body:**
```
grant_type = password
username = {client_user in Base64 format}
password = {client_password in Base64 format}
```

### Responses


**Sucesso (OK: 200):**

Exemplo de retorno com sucesso:
```
{
  "access_token": "sk3bnOJVGQy7LTECXLE_tfCXc8XFeppOL4qoomMBVzCpVjH4ifgFNX064CxCT6wRCN5Z1adnQyev2-S_WqRrojTE_SrfnGsBh2_6Q0rf0xf9shTMx0RgzMVKfGekpNyZ7DAMSIFRpEngxdnH_CF69feDc2gqS675tZtkGVl_0wq3hXutEQrenFzh6LszlVIG",
  "token_type": "bearer",
  "expires_in": 604799
}
```

**Erro de usuário/senha (BadRequest: 400):**

Exemplo de retorno com algum erro de usuário/senha:

```
{
  "error": "invalid_grant",
  "error_description": "The user name or password is incorrect."
}
```
**Erro (BadRequest: 400):**

Exemplo de erro na estrutura do request

```
{
  "error": "unsupported_grant_type"
}
```

## Leads

Permite o envio de leads

### Request

**Url:** 
```
http://{endpoint}/api/lead
```

**Method:**
```
POST
```

**Request Headers:**
```
Authorization = Bearer {token gerado anteriormente em api/token}
```

Exemplo

```
Authorization = Bearer sk3bnOJVGQy7LTECXLE_tfCXc8XFeppOL4qoomMBVzCpVjH4ifgFNX064CxCT6wRCN5Z1adnQyev2-S_WqRrojTE_SrfnGsBh2_6Q0rf0xf9shTMx0RgzMVKfGekpNyZ7DAMSIFRpEngxdnH_CF69feDc2gqS675tZtkGVl_0wq3hXutEQrenFzh6LszlVIG
```

**Request Body:**
```
{
    "LeadSource_Name": "",
    "CompanyName": "",
    "DealerName": "",
    "DealerStoreName": "",
    "ProductType": 1,
    "ProductBrandName": "",
    "ProductModelName": "",
    "ProductFullName": "",
    "ProductModelYear": "",
    "ProductManufactoringYear": "",
    "ProductColor": "",
    "ProductLicencePlate": "",
    "ProductPrice": "",
    "CustomerName": "",
    "CustomerEmail":"",
    "CustomerPhone":"",
    "CustomerMobilePhone": "",
    "CustomerCity": "",
    "CustomerState": "",
    "CustomerFiscalDocument": "",
    "CustomerMessage": ""
}
```
Exemplo:
```
{
    "LeadSource_Name": "Webmotors",
    "CompanyName": "Grupo vNext",
    "DealerName": "Ford vNext",
    "DealerStoreName": "Store of vNext",
    "ProductType": 1,
    "ProductBrandName": "Ford",
    "ProductModelName": "Ecosport",
    "ProductFullName": "Ford Ecosport 1.6 8V XLT FREESTYLE",
    "ProductModelYear": "2018",
    "ProductManufactoringYear":"2018",
    "ProductColor": "PRETO",
    "ProductLicencePlate": "ABC-1234",
    "ProductPrice": "R$ 99.900,00",
    "CustomerName": "Customer Name",
    "CustomerEmail": "customeremail@gmail.com",
    "CustomerPhone": "11 5555 5555",
    "CustomerMobilePhone": "11 9 9999 9999",
    "CustomerCity": "São Paulo",
    "CustomerState": "SP",
    "CustomerFiscalDocument":"299.299.299-99",
    "CustomerMessage": "Customer message and other informations"
}
```
### Responses


**Sucesso (OK: 200):**

Exemplo de retorno com sucesso:
```
{
    "success": true,
    "message": "Lead created successfully",
    "type": "info",
    "apiType": "LeadCreated"
}
```
**Erro (Unauthorized: 401):**

Exemplo de erro de token inválido ou expirado

```
{
    "message": "Authorization has been denied for this request."
}
```

**Erro de falha em algum campo obrigatório (BadRequest: 400):**

Exemplo de retorno com algum erro de usuário/senha:

```
{
    "success": false,
    "message": "<model.CustomerEmail: The CustomerEmail field is required.>",
    "type": "error",
    "apiType": "ModelIsNull"
}
```
