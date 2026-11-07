# Testes de Autenticação em API com Supabase e Postman

## 1. Introdução

Este projeto apresenta a realização de testes de caixa cinza em uma API de autenticação, utilizando o Supabase como ambiente de autenticação e o Postman Desktop para configuração, execução e validação das requisições HTTP.

A atividade teve como foco verificar o comportamento da autenticação de usuários, analisando respostas da API, códigos de status HTTP, mensagens de erro e retorno de tokens de acesso.

Foram realizados testes com diferentes cenários, incluindo autenticação válida, senha incorreta, usuário inexistente, campos vazios e credenciais inválidas.

## 2. Objetivo da Atividade

O objetivo desta atividade foi compreender e aplicar testes de caixa cinza em APIs de autenticação, utilizando ferramentas de mercado para validar o funcionamento de requisições HTTP.

Durante a atividade, foram realizadas as seguintes etapas:

- Utilização de um ambiente de autenticação no Supabase;
- Utilização de um usuário previamente cadastrado e confirmado;
- Configuração de requisições HTTP no Postman;
- Utilização de variáveis de ambiente;
- Execução de testes de autenticação;
- Validação de respostas JSON e códigos HTTP;
- Registro dos resultados obtidos em uma planilha.

## 3. Configuração do Supabase

Para a realização desta atividade, foi utilizado o ambiente Supabase previamente criado para o projeto Eletricitrus, conforme autorização concedida pelo professor em sala de aula.

O ambiente utiliza autenticação por e-mail e senha, permitindo realizar operações de cadastro e autenticação de usuários.

Foi utilizado um usuário previamente cadastrado e confirmado para executar os cenários de teste.

Para a comunicação com a API, foram utilizados os seguintes recursos:

- **API URL:** endereço do projeto Supabase;
- **API KEY:** chave pública utilizada nas requisições;
- **Autenticação:** e-mail e senha;
- **Usuário de teste:** usuário cadastrado e confirmado no ambiente.

O objetivo dessa configuração foi disponibilizar um ambiente funcional para testar e validar os processos de autenticação por meio de requisições HTTP no Postman.

## 4. Configuração do Postman

Foi utilizado o Postman Desktop para configurar e executar as requisições de autenticação.

Inicialmente, foi criado um Workspace para organizar os testes. Em seguida, foi configurado um Environment chamado `Supabase`, contendo as variáveis necessárias para a execução das requisições.

As variáveis utilizadas foram:

| Variável | Descrição |
|---|---|
| `base_url` | URL do projeto Supabase |
| `api_key` | Chave pública da API |
| `email` | E-mail do usuário de teste |
| `password` | Senha do usuário de teste |

A utilização dessas variáveis facilita a reutilização das requisições e evita a necessidade de inserir manualmente as informações em cada teste.

Foi criada uma coleção chamada `Testes de Autenticacao - Supabase`, contendo cinco requisições independentes, uma para cada cenário de teste.

A coleção exportada está armazenada no diretório `postman/`.

## 5. Configuração das Requisições

Para os testes, foi utilizada uma requisição HTTP do tipo **POST**, responsável por realizar a autenticação do usuário no Supabase.

### Endpoint utilizado

`{{base_url}}/auth/v1/token?grant_type=password`

### Método HTTP

`POST`

### Headers utilizados

| Header | Valor |
|---|---|
| `apikey` | `{{api_key}}` |
| `Authorization` | `Bearer {{api_key}}` |
| `Content-Type` | `application/json` |

### Body JSON

O corpo da requisição utiliza o formato JSON para enviar as credenciais do usuário:

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

As variáveis permitem utilizar diferentes entradas em cada cenário, mantendo a mesma estrutura de requisição.

### Finalidade

A requisição tem como finalidade enviar as credenciais do usuário ao endpoint de autenticação do Supabase, permitindo verificar se os dados informados são válidos.

Quando a autenticação é realizada corretamente, a API retorna informações do usuário e um token de acesso. Quando as credenciais são inválidas, a API retorna uma resposta de erro.

## 6. Execução dos Testes

Foram executados cinco cenários de teste para verificar o comportamento da API em diferentes situações de autenticação.

Os testes foram organizados individualmente na coleção do Postman e possuem scripts de validação automática na etapa Post-response.

### Cenários executados

**01 — Login válido**

Foi utilizado o e-mail e a senha de um usuário cadastrado e confirmado no Supabase.

Resultado esperado: HTTP 200 e retorno de token de acesso.

**02 — Senha incorreta**

Foi utilizado o e-mail do usuário cadastrado, porém com uma senha incorreta.

Resultado esperado: rejeição da autenticação, HTTP 400 e ausência de token de acesso.

**03 — Usuário inexistente**

Foi informado um e-mail que não possui cadastro no ambiente Supabase.

Resultado esperado: acesso negado, HTTP 400 e ausência de token de acesso.

**04 — Campos vazios**

Foram enviados os campos de e-mail e senha sem preenchimento.

Resultado esperado: rejeição da requisição, HTTP 400 e ausência de token de acesso.

**05 — Credenciais inválidas (e-mail em formato inválido)**

Foi informado um endereço de e-mail em formato inválido.

Resultado esperado: rejeição da autenticação, HTTP 400 e ausência de token de acesso.

### Validações realizadas

Durante a execução, foram verificados:

- Códigos de status HTTP;
- Respostas retornadas em JSON;
- Mensagens e códigos de erro;
- Presença ou ausência do token de acesso;
- Tipo de token retornado na autenticação válida.

## 7. Registro dos Testes

Os resultados dos cenários executados foram organizados em uma planilha, contendo os seguintes campos:

- ID do teste;
- Cenário;
- Entrada utilizada;
- Resultado esperado;
- Resultado obtido;
- Status;
- Observações.

O registro permite acompanhar os resultados de cada cenário, identificar comportamentos inesperados e manter evidências documentadas da execução.

A planilha está disponível no diretório `planilha/`.

**Arquivo:** `planilha/resultados-testes-autenticacao-supabase.xlsx`

## 8. Resultados Obtidos

Após a execução dos cinco cenários, foram obtidos os seguintes resultados:

| ID | Cenário | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|
| 01 | Login válido | HTTP 200 e token | HTTP 200 e token retornado | Aprovado |
| 02 | Senha incorreta | Rejeição da autenticação | HTTP 400 | Aprovado |
| 03 | Usuário inexistente | Acesso negado | HTTP 400 | Aprovado |
| 04 | Campos vazios | Erro na requisição | HTTP 400 | Aprovado |
| 05 | Credenciais inválidas | Rejeição da autenticação | HTTP 400 | Aprovado |

Os resultados demonstraram que a API permitiu a autenticação com credenciais válidas e rejeitou as solicitações com dados inválidos ou incompletos.

Os scripts de validação do Postman foram utilizados para verificar automaticamente os códigos HTTP, as respostas JSON e a presença ou ausência do token de acesso.

As evidências individuais de cada cenário estão disponíveis na pasta `prints/`:

- `01-login-valido-200.jpg`
- `02-senha-incorreta-400.jpg`
- `03-usuario-inexistente-400.jpg`
- `04-campos-vazios.jpg`
- `05-email-invalido-400.jpg`

## 9. Conclusão

A realização desta atividade permitiu compreender melhor o funcionamento de APIs de autenticação e a aplicação de testes de caixa cinza em serviços que utilizam requisições HTTP.

Os cinco cenários propostos foram executados no Postman, permitindo verificar tanto o comportamento esperado para uma autenticação válida quanto a rejeição de solicitações com credenciais incorretas, usuários inexistentes, campos vazios e e-mails em formato inválido.

Durante o desenvolvimento, foi possível praticar a configuração de ambientes, utilização de variáveis, organização de coleções e criação de scripts para validação automática dos resultados.

Uma das dificuldades encontradas esteve relacionada à configuração inicial das requisições e à organização dos testes no Postman. Após os ajustes, os cenários foram organizados individualmente e executados com sucesso.

Como melhoria futura, poderiam ser implementados novos cenários de teste, validações adicionais de segurança, testes de limites de requisições e verificações de diferentes comportamentos da API.

Conclui-se que os testes de caixa cinza são importantes para avaliar o funcionamento de APIs, pois permitem analisar as entradas, saídas e aspectos conhecidos da estrutura interna da comunicação, contribuindo para a identificação de falhas e para a melhoria da qualidade do software.