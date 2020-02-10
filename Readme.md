# Documentação API do LeadHub

Documentação para uso da API do LeadHub destinada a  parceiros e clientes.

Saiba mais sobre o LeadHub em [https://www.leadhub.com.br](https://www.leadhub.com.br)

## Itens

1. [Tecnologia](#tecnologia)
2. [Token](#token)
   - [Request](#request)
   - [Responses](#responses)
3. [Leads](#leads)
   - [Request](#request-1)
   - [Responses](#responses-1)

## Tecnologia

A API utiliza padrão `REST`, utiliza estrutura `JSON` para envio e recebimento de dados e é de fácil implementação em sua linguagem de programação preferida.

### Endpoints

Solicite ao *nosso time técnico* os endereços correspontentes à última versão da API

## Token

A autenticação é feita através de token `OAUTH` e todas as chamadas serão autenticadas com esse token. O token de acesso tem uma validade de 24 horas.

O usuário/senha utilizado no header em `Basic Authentication` é usado para validar a origem de integração, solicite o usuário e senha do seu ambiente ao *nosso time técnico*.

O usuário/senha utilizado no body em `grant_type` é usado para espeficar o `domain` em que os dados serão integrados.

### Request

**Url:** 
```
http://{endpoint}/token
```

**Method:**
```
POST
```

**Request Headers:**
```
Authorization = Basic {api_user:api_password pair in Base64 format}
```
Exemplo:
```
Authorization = Basic dXNlcjpwYXNzd29yZA==
```
**Request Body:**
```
grant_type = password
username = {client_user in Base64 format}
password = {client_password in Base64 format}
```
Exemplo:
```
username = dXNlcg==
password = cGFzc3dvcmQ=
```

### Responses


**Sucesso (OK: 200):**

Exemplo de retorno com sucesso:
```json
{
  "access_token": "sk3bnOJVGQy7LTECXLE_tfCXc8XFeppOL4qoomMBVzCpVjH4ifgFNX064CxCT6wRCN5Z1adnQyev2-S_WqRrojTE_SrfnGsBh2_6Q0rf0xf9shTMx0RgzMVKfGekpNyZ7DAMSIFRpEngxdnH_CF69feDc2gqS675tZtkGVl_0wq3hXutEQrenFzh6LszlVIG",
  "token_type": "bearer",
  "expires_in": 604799
}
```

**Erro de usuário/senha (BadRequest: 400):**

Exemplo de retorno com algum erro de usuário/senha:

```json
{
  "error": "invalid_grant",
  "error_description": "The user name or password is incorrect."
}
```
**Erro (BadRequest: 400):**

Exemplo de erro na estrutura do request

```json
{
  "error": "unsupported_grant_type"
}
```

## Leads

Permite o envio de leads

### Request

**Url:** 
```
http://{endpoint}/lead
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
```json
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
```json
{
    "LeadSource_Name": "Chat",
    "CompanyName": "Grupo vNext",
    "DealerName": "Ford vNext",
    "DealerStoreName": "Ford vNext Perdizes",
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

Especificação dos campos

> **(*)**  Campos obrigatórios

 | Campo                        | Descrição                                                                   | Tipo     | Limite de caracteres|
 |-----------------------------    |---------------------------------------------------------------------------- |----------|---------------------|
 | LeadSource_Name                 | Origem do lead                                                              | string   | 100  |
 | CompanyName   **(*)**               | Organização ou nome do grupo                                                | string   | 100   |
 | DealerName     **(*)**              | Concessinária escolhida pelo cliente                                        | string   |  100  |
| DealerStoreName    **(*)**           | Loja escolhida pelo cliente                                                 | string   | 100  |
| ProductType       **(*)**            | Tipo do produto (Para automotivo: 1 - Seminovo, 2 - Novo, 3 - Venda Direta  | inteiro  |   |
 | ProductBrandName                | Marca do produto                                                            | string   | 50  |
 | ProductModelName                | Modelo do produto                                                           | string   |  50 |
 | ProductFullName                  | Nome completo do produto incluindo marca, modelo e versão                   | string   | 100  |
 | ProductModelYear                | Ano do modelo do produto                                                    | string   | 4  |
 | ProductManufactoringYear        | Ano de fabricação do produto                                                | string   | 4  |
 | ProductColor                    | Cor do produto                                                              | string   | 50  |
 | ProductLicencePlate             | Placa ou Chassi do produto                                                  | string   | 80  |
 | ProductPrice                    | Preço do produto                                                            | string   | 50  |
 | CustomerName **(*)**                  | Nome do cliente                                                            | string   | 100  |
 | CustomerEmail  **(*)**                 | Email do cliente                                                            | string   | 100  |
 | CustomerPhone **(*)**                  | Telefone do cliente                                                         | string   | 27  |
 | CustomerMobilePhone             | Celular do cliente                                                          | string   |  27 |
 | CustomerCity                    | Cidade do cliente                                                           | string   |  100 |
 | CustomerState                   | Estado do cliente                                                           | string   | 50  |
 | CustomerFiscalDocument          | CPF ou CNPJ do cliente                                                      | string   | 30  |
 | CustomerMessage                 | Mensagem do cliente                                                         | string   | 4000  |

### Responses


**Sucesso (OK: 200):**

Exemplo de retorno com sucesso:
```json
{
    "success": true,
    "message": "Lead created successfully id: 9999999",
    "type": "info",
    "apiType": "LeadCreated"
}
```
**Erro (Unauthorized: 401):**

Exemplo de erro de token inválido ou expirado

```json
{
    "message": "Authorization has been denied for this request."
}
```

**Erro de falha em algum campo obrigatório (BadRequest: 400):**

Exemplo de retorno com algum erro de usuário/senha:

```json
{
    "success": false,
    "message": "<model.CustomerEmail: The CustomerEmail field is required.>",
    "type": "error",
    "apiType": "ModelIsNull"
}
```
