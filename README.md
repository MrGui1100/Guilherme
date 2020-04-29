<a name="top"></a>
# Example v0.0.0

apiDoc basic example

- [Integracao_com_a_LTM](#Integracao_com_a_LTM)
	- [A API de resgate e resonsavel por criar os vales na plataforma](#A-API-de-resgate-e-resonsavel-por-criar-os-vales-na-plataforma)
	- [API responsavel por aprovar os vales gerados na plataforma](#API-responsavel-por-aprovar-os-vales-gerados-na-plataforma)
	


# <a name='Integracao_com_a_LTM'></a> Integracao_com_a_LTM

## <a name='A-API-de-resgate-e-resonsavel-por-criar-os-vales-na-plataforma'></a> A API de resgate e resonsavel por criar os vales na plataforma
[Back to top](#top)

```
POST /LTM/resgate
```

### Headers
| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| Authorization | `String` | <p>Autenticaï¿½ï¿½o no padrï¿½o Auth Basic</p> |

### Parameters - `Parameter`
| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| CNPJ | `String` | <p>Portador do vale gerado na plataforma, precisa estar cadastrado</p> |
| email | `String` |  |
| razaoSocial | `String` |  |
| creditos | `Number` | <p>Valor do vale ï¿½ gerado na plataforma</p> |

### Success response

#### Success response - `Success 200`
| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| success | `Boolean` |  |
| CNPJ | `String` |  |
| Codigo | `String` | <p>Cï¿½digo do vale gerado na plataforma. Deve ser passado como parï¿½metro ao endpoint /LTM/aprovacao para ser habilitado para uso</p> |

### Error response example

#### Error response example - `Autenticacao:`

```
HTTP/1.1 401 Authorization Required
{
    "success": false,
    "code": "",
    "message": "Request sent by the client could not be authenticated"
}
```

#### Error response example - `Dados invalidos:`

```
HTTP/1.1 400 Bad Request
{
    "success": false,
    "code": "parametros.invalidos",
    "message": "Parï¿½metros invï¿½lidos"
}
```

#### Error response example - `Codigo IFC nao encontrado:`

```
HTTP/1.1 400 Bad Request
{
    "success": false,
    "code": "cnpj.nao.encontrado",
    "message": "CNPJ nï¿½o cadastrado"
}
```

#### Error response example - `Codigo LTM nao encontrado:`

```
HTTP/1.1 400 Bad Request
{
  "success": false,
  "code": "voucher.erro.geracao",
  "message": "Erro inesperado ao tentar gerar voucher"
}
```

## <a name='API-responsavel-por-aprovar-os-vales-gerados-na-plataforma'></a> API responsavel por aprovar os vales gerados na plataforma
[Back to top](#top)

```
POST /LTM/aprovacao
```

### Headers
| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| Authorization | `String` | <p>Autenticaï¿½ï¿½o no padrï¿½o Auth Basic</p> |

### Parameters - `Parameter`
| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| Codigo | `String` | <p>Cï¿½digo do vale gerado na plataforma. Retornado no endpoint /LTM/resgate</p> |
| CodigoLTM | `String` | <p>Cï¿½digo gerado pela LTM</p> |

### Success response

#### Success response - `Success 200`
| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| success | `Boolean` |  |

### Error response example

#### Error response example - `Autenticacao:`

```
HTTP/1.1 401 Authorization Required
{
    "success": false,
    "code": "",
    "message": "Request sent by the client could not be authenticated"
}
```

#### Error response example - `Dados invalidos:`

```
HTTP/1.1 400 Bad Request
{
    "success": false,
    "code": "parametros.invalidos",
    "message": "Parï¿½metros invï¿½lidos"
}
```

#### Error response example - `Codigo IFC nao encontrado:`

```
HTTP/1.1 400 Bad Request
{
    "success": false,
    "code": "voucher.nao.encontrado",
    "message": "Voucher nï¿½o encontrado"
}
```

#### Error response example - `Codigo IFC ja aprovado:`

```
HTTP/1.1 400 Bad Request
{
    "success": false,
    "code": "voucher.erro.aprovado",
    "message": "Voucher jï¿½ aprovado"
}
```

#### Error response example - `Erro inesperado ao aprovar voucher:`

```
HTTP/1.1 400 Bad Request
{
  "success": false,
  "code": "voucher.erro.aprovacao",
  "message": "Erro inesperado ao tentar aprovar o voucher"
}
```
