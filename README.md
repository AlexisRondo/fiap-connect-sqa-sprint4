# FIAP Connect — SQA Sprint 4

Entrega da disciplina **Compliance & Quality Assurance** da Sprint 4 do Challenge Oracle FIAP.

## Integrantes

| Nome                           | RM     | Turma  |
| ------------------------------ | ------ | ------ |
| Alexis Rondo                   | 560384 | 2TDSPS |
| Vinicius Rodrigues de Oliveira | 559611 | 2TDSPS |

---

## Sistema testado

API REST .NET do FIAP Connect hospedada em AWS EC2.

- **API em producao:** https://44-214-247-152.sslip.io
- **Swagger:** https://44-214-247-152.sslip.io/swagger
- **Repositorio do sistema:** https://github.com/Sprint1-Fiap-Connect/fiap-connect-dotnet-sprint3

---

## Parte A — Plano de testes manuais (Azure Boards)

12 Test Cases foram criados na plataforma Azure DevOps Boards, cobrindo as funcionalidades principais da API .NET do FIAP Connect.

**Link do Azure DevOps:**
https://dev.azure.com/RM560384/FIAP-Connect

**Shared Query contendo os 12 Test Cases:**
https://dev.azure.com/RM560384/FIAP-Connect/_queries/query/cedfe4df-e89c-4655-9600-c0cadca22db2/

### Cobertura dos Test Cases

| Categoria                         | Quantidade |
| --------------------------------- | ---------- |
| Autenticacao (Firebase + JWT)     | 3          |
| Notificacoes (CRUD + canonizacao) | 5          |
| Conversas                         | 2          |
| Historico de buscas               | 1          |
| Health Check                      | 1          |
| **Total**                         | **12**     |

Cada Test Case contem:

1. Titulo e descricao do objetivo
2. Dados de entrada (endpoint, headers, body)
3. Dados de saida esperados (status code, estrutura do response)
4. Procedimento detalhado em steps (Action + Expected Result)

---

## Parte B — Automacao com Postman

Collection com 4 requests automatizados cobrindo o fluxo end-to-end da API.

### Requests da collection

1. **Login (gerar JWT)** - POST /api/auth/login
2. **Criar Notificacao** - POST /api/notificacoes
3. **Listar Notificacoes** - GET /api/notificacoes (com paginacao e HATEOAS)
4. **Deletar Notificacao** - DELETE /api/notificacoes/{id}

### Testes implementados

**17 asserts** distribuidos entre os 4 requests, validando:

- Status codes (200, 201, 204)
- Estrutura do response (campos obrigatorios, formato ObjectId, paginacao, HATEOAS)
- Regras de negocio (canonizacao de RM, encadeamento de variaveis entre requests)
- Performance (tempo de resposta abaixo de 5 segundos)

### Variaveis dinamicas

A collection utiliza variaveis de environment preenchidas dinamicamente entre os requests:

- `jwt` - salvo apos login, usado nos demais requests
- `notificacaoId` - salvo apos criar notificacao, usado em listar e deletar

### Como executar

1. Importar `FIAP-Connect-SQA-Sprint4.postman_collection.json` no Postman
2. Importar `FIAP-Connect-Prod.postman_environment.json` como environment
3. Preencher a variavel `idToken` com um idToken Firebase valido (obtido via login no app Mobile)
4. Selecionar o environment `FIAP Connect Prod`
5. Executar a collection completa via **Collection Runner**

---

## Video de demonstracao

Video nao listado no YouTube mostrando configuracao e execucao da automacao:

[Vídeo de demonstração Postman](https://youtu.be/MRoEkkRDtBk)

[Usando Swagger e com integração real com MongoDB](https://youtu.be/3-qGD7G8NU4)    
     
---

## Tecnologias utilizadas

- **Azure DevOps Boards** - Gerenciamento de Test Cases manuais
- **Postman** - Automacao de testes de API
- **Postman Collection Runner** - Execucao em batch
