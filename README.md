# Introdução
Esta atividade foi realizada afim de demonstrar como deve ser realizado um teste caixa cinza, utilizando as plataformas supabase e postman

# Objetivo da Atividade
O objetivo desta atividade é compreender, configurar e aplicar testes funcionais em um endpoint de autenticação. O foco é analisar o comportamento da API (status HTTP, body JSON e access token) mediante o envio de diferentes cenários de dados (corretos, incorretos, vazios e mal formatados), consolidando o conceito de testes caixa cinza.


# Configuração do Supabase
* **Como o projeto foi criado:** [Conta criada via GitHub no site do Supabase e provisionamento de um novo projeto.]
* **Tipo de autenticação utilizada:** Autenticação padrão via e-mail e senha.
* **Como o usuário foi criado:** [Criado manualmente no painel interno do Supabase, na aba Authentication > Users.]
* **Objetivo da configuração:** Fornecer um banco de dados real e um endpoint de autenticação funcional para validar as requisições.

### Evidências - Supabase
![Projeto Criado](/imagens-testes/criado-supa.png)
![Painel do Supabase](/imagens-testes/project-settings.png)
![Usuário Criado](/imagens-testes//users.png)

---

Ferramenta utilizada: Postman (Desktop).

1. Criar um Workspace/Collection para a atividade.
2. Criar um Environment para armazenar variáveis reutilizáveis.

Variáveis usadas no Environment:

| Variável   | Descrição                                             |
| ---------- | ----------------------------------------------------- |
| `base_url` | URL base da API do Supabase                           |
| `api_key`  | Chave de API utilizada para autenticar as requisições |
| `email`    | E-mail do usuário criado no Supabase                  |
| `password` | Senha do usuário criado no Supabase                   |


### Evidências - Postman
![Workspace Criado](/imagens-testes/ambiente-supá.png)
![Environment e Variáveis](/imagens-testes/headers.png)

---

Endpoint utilizado para autenticação (login por senha):

```
POST {{base_url}}/auth/v1/token?grant_type=password
```

Headers necessários:

| Header          | Valor                |
| --------------- | -------------------- |
| `apikey`        | `{{api_key}}`        |
| `Authorization` | `Bearer {{api_key}}` |
| `Content-Type`  | `application/json`   |


**Exemplo de Header e Body:**
* `apikey`: [Sua chave ou variável aqui]
* `Content-Type`: `application/json`

##json
{
  "email": "usuario@email.com",
  "password": "123456"
}

## Execução dos Testes

Foram executados testes de caixa cinza com os seguintes objetivos de verificação:

- Verificar status HTTP retornado pela API.
- Analisar a estrutura das respostas JSON.
- Confirmar mensagens de erro em cenários de falha.
- Validar retorno do `access_token` em login válido.

Cenários testados:

| Cenário               | Entrada Utilizada                      | Resultado Esperado          |
| --------------------- | -------------------------------------- | --------------------------- |
| Login válido          | E-mail e senha corretos                | Status 200 + `access_token` |
| Usuário inexistente   | E-mail não cadastrado e senha qualquer | Acesso negado
| Senha incorreta       | E-mail correto e senha incorreta       | Erro de autenticação        |              |
| Campos vazios         | E-mail e senha vazios                  | Erro de validação           |
| Credenciais inválidas | E-mail e senha inválidos               | Mensagem de erro            |


Evidências dos testes (imagens disponíveis em `imagens-erros/`):

![Teste - login válido](/imagens-testes/200ok.png)

![Teste - senha incorreta](/imagens-testes/senha-errrada.png)

![Teste - e-mail inválido / usuário inexistente](/imagens-testes/email-errado.png)

![Teste - campos nulos/vazios](/imagens-testes/usuario-fantasma.png)

## Conclusão

A execução dos testes foi realizada corretamente no Postman, com cobertura dos cenários previstos (login válido, senha incorreta, usuário inexistente, campos vazios e credenciais inválidas), além do registro dos resultados em evidências e planilha.

