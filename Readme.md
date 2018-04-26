# LEADHUB - Documenta��o API

## Descri��o

Documenta��o para uso dos endpoints da API para parceiros e clientes do LEADHUB

[http://www.leadhub.com.br](http://www.leadhub.com.br)

## Tecnologia

A API utiliza padr�o `REST`, utiliza nota��o `JSON` para envio e recebimento de dados e � de f�cil implementa��o em sua linguagem de programa��o preferida.

## Endpoints

Solicite ao *nosso time t�cnico* os endere�os correspontentes � �ltima vers�o da API

## Autentica��o

A autentica��o � feita atrav�s de token `OAUTH` e todas as chamadas ser�o autenticadas com esse token. O token de acesso tem uma validade de 24 horas.
Basic Authentication com as chaves criptografadas em Base64, solicite o usu�rio e senha do seu ambiente ao *nosso time t�cnico*.

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

**Erro de usu�rio/senha (BadRequest: 400):**

Exemplo de retorno com algum erro de usu�rio/sena:

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