<p align="center">
  <img src="logo-magazord.png" width="240" />
</p>

---

# Teste para vaga de Coordenador de Qualidade – Magazord

Este repositório tem como objetivo avaliar candidatos à vaga de Coordenador de Qualidade na Magazord.

O teste é focado em testes automatizados, arquitetura de testes, estratégia de qualidade, integrações e boas práticas aplicadas a cenários reais.

## 📋 Instruções Gerais

- Responda às questões teóricas de forma clara e objetiva
- Para cada questão prática, crie um projeto executável
- Utilize Cypress,Playwright, Robot ou o framework à sua escolha
- Organize seu código de forma profissional (Page Objects, helpers, etc.)
- Inclua README com instruções de execução de cada teste 
- Crie os casos de teste para cada teste prático que será desenvolvido
- **Prazo de entrega:** 2 dias corridos
- Não serão aceitas alterações após o envio

## 📦 Estrutura de Entrega Esperada

```
seu-repositorio/
├── README.md
├── package.json
├── cypress.config.js (ou playwright.config.js)
├── parte1-api/
│   └── questao1.1/
├── parte2-e2e/
│   └── questao2.1/
├── parte3-arquivos/
│   └── questao3.1/
├── parte4-mobile/
│   └── questao4.1/
│       └── RESPOSTA_TEORICA.md
└── parte5-mocks/
    └── questao5.1/
        └── RESPOSTA_TEORICA.md
```

> ⚠️ As Partes 4 e 5 são **somente teóricas** — não é necessário implementar código ou configurar ambiente para elas. O foco é avaliar raciocínio, conhecimento de ferramentas e capacidade de arquitetar uma solução.

---
 
## Casos de teste

Para cada cenário de teste prático apresentado nas questões, você deve:
Criar casos de teste automatizados que cubram adequadamente o cenário proposto.

Você é responsável por:

- Definir quais casos de teste são necessários
- Determinar a quantidade de testes
- Escolher quais cenários cobrir (sucesso, erro, edge cases, etc)
- Estruturar a organização dos testes

Não serão fornecidos detalhes de implementação ou lista de casos esperados.
A avaliação considerará sua capacidade de:

- Identificar cenários relevantes
- Criar cobertura adequada
- Estruturar testes de forma profissional
- Demonstrar pensamento crítico sobre qualidade

O arquivo com os casos de teste pode ser encaminhado no repositório em formato DOCX, PDF ou TXT.

Em resumo: Leia o cenário, analise o que precisa ser testado e crie os testes que você julgar necessários.

---

# PARTE 1: TESTES API

## Questão 1.1 - Rate Limiting e Autenticação com Token

### 📖 Contexto
Você precisa testar uma API REST que possui rate limiting de requisições, e também uma API que retorna um token de autenticação com tempo de expiração curto, usado em chamadas subsequentes.

### 💭 Perguntas Teóricas

**1.1.a)** Como você estruturaria seus testes automatizados para validar que o rate limiting está funcionando corretamente, e como testaria o comportamento quando o limite é excedido?

**1.1.b)** Como você implementaria um mecanismo simples para obter e reutilizar um token de autenticação entre os testes, evitando fazer login a cada teste?

**1.1.c)** Como você detectaria que um token expirou e trataria esse cenário no seu teste?

### 🔨 Teste Prático

**API 1 (Rate Limiting):** GitHub API - https://api.github.com

A GitHub API tem rate limiting de:
- 60 requisições/hora (sem autenticação)
- 5000 requisições/hora (com autenticação)

**Endpoint para testar:**
```
GET https://api.github.com/users/github
```

**API 2 (Token):** ReqRes API - https://reqres.in

```javascript
// Login
POST https://reqres.in/api/login
Body: { "email": "eve.holt@reqres.in", "password": "cityslicka" }
Response: { "token": "QpwL5tke4Pnpja7X4" }

// Requisição autenticada (qualquer endpoint GET)
GET https://reqres.in/api/users/2
Headers: { "Authorization": "Bearer {token}" }
```

**Implemente:**

1. Um teste que valida os headers de rate limiting (`X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`) na API do GitHub
2. Um teste que detecta quando o rate limit foi atingido (status 403)
3. Um fluxo simples de login via ReqRes que obtém o token e o reutiliza em uma requisição autenticada
4. Um teste que simule a expiração do token (pode ser um valor fixo curto, ex: 2 minutos) e valide o tratamento do erro

**Entregáveis:**
- `parte1-api/questao1.1/RESPOSTA_TEORICA.md` - Suas respostas teóricas
- `parte1-api/questao1.1/testes/api.spec.js` - Testes implementados
- `parte1-api/questao1.1/testes/utils/api-helper.js` - Helper de rate limit e token

---

# PARTE 2: TESTES E2E

## Questão 2.1 - Fluxo de Checkout

### 📖 Contexto
Você precisa testar um fluxo de checkout que envolve:
- Adicionar produtos ao carrinho
- Aplicar cupom de desconto (que só pode ser usado uma vez)
- Processar pagamento
- Verificar confirmação de pedido

### 💭 Perguntas Teóricas

**2.1.a)** Como você garantiria que cada execução de teste use um cupom válido diferente?

**2.1.b)** Como você validaria a confirmação do pedido sem depender de email real?

### 🔨 Teste Prático

**Site a ser utilizado:** https://www.saucedemo.com

**Implemente:**

1. Fluxo completo de checkout (login → adicionar produtos → checkout → finalizar)
2. Geração dinâmica de dados para cada execução (nome, sobrenome, CEP)
3. Validação da confirmação de pedido
4. Limpeza após cada teste (cookies, localStorage)

**Credenciais:**
- Username: `standard_user`
- Password: `secret_sauce`

**Entregáveis:**
- `parte2-e2e/questao2.1/RESPOSTA_TEORICA.md`
- `parte2-e2e/questao2.1/testes/checkout-flow.spec.js`
- `parte2-e2e/questao2.1/testes/pages/checkout-page.js` - Page Object
- `parte2-e2e/questao2.1/testes/fixtures/checkout-data.js` - Gerador de dados

---

# PARTE 3: TESTES COM ARQUIVOS

## Questão 3.1 - Importação de CSV

### 📖 Contexto
Sistema que importa arquivos CSV com 1000+ linhas e valida:
- Formato dos dados
- Regras de negócio
- Duplicatas
- Relacionamentos

### 💭 Perguntas Teóricas

**3.1.a)** Como validaria que todas as 1000 linhas foram processadas corretamente?

**3.1.b)** Como testaria cenários de erro (arquivo corrompido, dados inválidos)?

### 🔨 Teste Prático

**Site a ser utilizado:** https://the-internet.herokuapp.com/upload

**Implemente:**

1. Gerador de CSV dinâmico com:
   - 10 linhas (teste pequeno)
   - 100 linhas (teste médio)
   - 1000 linhas (teste grande)

2. Upload de arquivo válido

3. Upload de arquivo inválido:
   - CSV vazio
   - CSV com formato incorreto
   - CSV com dados malformados

4. Validação de upload bem-sucedido

**Entregáveis:**
- `parte3-arquivos/questao3.1/RESPOSTA_TEORICA.md`
- `parte3-arquivos/questao3.1/testes/csv-upload.spec.js`
- `parte3-arquivos/questao3.1/testes/utils/csv-generator.js` - Gerador de CSV
- `parte3-arquivos/questao3.1/testes/fixtures/` - Exemplos de CSV (válido, inválido, corrompido)


**Exemplo de CSV a ser gerado:**
```csv
nome,email,idade,cidade
João Silva,joao@email.com,30,São Paulo
Maria Santos,maria@email.com,25,Rio de Janeiro
```

---

# PARTE 4: TESTES MOBILE (TEÓRICA)

## Questão 4.1 - Automação Mobile

### 📖 Contexto
Aplicativo mobile (iOS e Android) que usa:
- Geolocalização
- Câmera
- Notificações push
- Storage offline
- Sincronização

### 💭 Perguntas Teóricas

Esta questão é **somente teórica** — não é necessário implementar nenhum código ou configurar ambiente. Responda com profundidade técnica e justifique suas escolhas.

**4.1.a)** Qual ferramenta você escolheria para automação mobile (Appium, Detox, Maestro, etc.) e por quê? Compare pelo menos 2 opções considerando o contexto descrito.

**4.1.b)** Como você mockaria geolocalização, câmera e notificações push em testes automatizados? Descreva a abordagem para cada um.

**4.1.c)** Qual estratégia você usaria para executar os mesmos testes em iOS e Android, minimizando duplicação de código?

**4.1.d)** Descreva, em alto nível, como seria o setup de ambiente para rodar esses testes localmente e em CI/CD (passos principais, sem precisar executar).

**4.1.e)** Como você validaria sincronização de dados e comportamento offline sem depender de um backend real?

**Entregáveis:**
- `parte4-mobile/questao4.1/RESPOSTA_TEORICA.md`

---

# PARTE 5: MOCKS E INTEGRAÇÕES (TEÓRICA)

## Questão 5.1 - Mocks de APIs Externas

### 📖 Contexto
Seu sistema integra com marketplaces (Mercado Livre, Amazon) via API para:
- Publicar produtos
- Atualizar preços
- Processar pedidos
- Atualizar estoque

### 💭 Perguntas Teóricas

Esta questão é **somente teórica** — não é necessário implementar mock server, código ou schemas. Responda com profundidade técnica e justifique suas escolhas.

**5.1.a)** Como você testaria essas integrações sem afetar os ambientes reais dos marketplaces?

**5.1.b)** Como implementaria uma estratégia de mock para simular respostas? Qual(is) ferramenta(s) você usaria (MSW, JSON Server, WireMock, etc.) e por quê?

**5.1.c)** Descreva como você simularia, em nível de mock, os seguintes cenários: erro 500, timeout e rate limiting (429). O que cada um desses testes deve validar no seu sistema?

**5.1.d)** Como você validaria que o payload enviado/recebido está no formato esperado (schema validation)? Onde essa validação entraria no seu pipeline de testes?

**5.1.e)** Qual sua visão sobre a diferença entre testes com mock e testes de contrato (contract testing) nesse cenário de integração com marketplaces? Quando usar cada um?

**Entregáveis:**
- `parte5-mocks/questao5.1/RESPOSTA_TEORICA.md`

---

OBS: Os links disponibilizados para os testes são apenas como referência e exemplo. Caso não consiga acessar algum deles ou queira utilizar outro, fique à vontade, desde que sejam públicos e estejam acessíveis no momento da execução do teste.


## O que será avaliado em cada teste

### Respostas Teóricas 
- Clareza e objetividade
- Profundidade técnica
- Exemplos práticos
- Conhecimento de boas práticas

### Código (Partes 1, 2 e 3)
- ✅ Testes executam sem erro
- ✅ Código limpo e organizado
- ✅ Uso de Page Objects / Helpers
- ✅ Tratamento de erros
- ✅ Comentários em código complexo
- ✅ README com instruções claras
- ✅ Boas práticas de automação

### Partes 4 e 5 (Teóricas)
- ✅ Profundidade técnica e domínio de ferramentas/conceitos
- ✅ Comparação de abordagens com justificativa (não só descrever, mas argumentar)
- ✅ Capacidade de pensar em arquitetura de solução sem precisar codar
- ✅ Clareza de escrita
---

# 📝 README.md Obrigatório

Seu repositório **DEVE** conter um README.md na raiz com:

```markdown
# Teste QA Sênior - [Seu Nome]

## Tecnologias Utilizadas
- Node.js v18+
- Cypress 13.x (ou Playwright 1.x)
- Outras...

## Instalação

\`\`\`bash
npm install
\`\`\`

## Execução dos Testes

### Todos os testes
\`\`\`bash
npm test
\`\`\`

### Por parte
\`\`\`bash
npm run test:parte1
npm run test:parte2
npm run test:parte3
# Partes 4 e 5 são teóricas, sem script de execução
\`\`\`

## Estrutura do Projeto

(Explique a organização das pastas)

## Observações

(Dificuldades encontradas, decisões técnicas, etc)
```

---

# ⏰ PRAZO E ENTREGA

- **Prazo:** 2 dias corridos a partir do recebimento
- **Formato:** Link do repositório Git (GitHub, GitLab, Bitbucket)

## ✅ Checklist antes de Enviar

- [ ] Todos os testes executam com `npm install && npm test`
- [ ] README.md está completo e claro
- [ ] Respostas teóricas estão nos arquivos RESPOSTA_TEORICA.md
- [ ] Código está organizado e comentado
- [ ] Commits git estão bem descritos
- [ ] Não há credenciais ou secrets no código
- [ ] Testei em uma máquina limpa (ou container)

---

# 📌 ANEXO: Recursos Úteis

## APIs Públicas Utilizadas
- GitHub API: https://docs.github.com/en/rest
- ReqRes API: https://reqres.in/
- Fake Store API: https://fakestoreapi.com/

## Sites para Testes
- Sauce Demo: https://www.saucedemo.com/
- The Internet: https://the-internet.herokuapp.com/

## Ferramentas Sugeridas
- Cypress: https://www.cypress.io/
- Playwright: https://playwright.dev/
- Robot Framework - https://robotframework.org/
- JSON Server: https://github.com/typicode/json-server
- MSW: https://mswjs.io/

## Documentação
- Cypress Best Practices: https://docs.cypress.io/guides/references/best-practices
- Playwright Best Practices: https://playwright.dev/docs/best-practices
- https://docs.robotframework.org/docs


<span style="color: red;"><strong>Observação: caso você avance para a próxima etapa da entrevista técnica, será importante estar preparado para executar os testes em seu próprio ambiente durante a avaliação. Dessa forma, poderemos acompanhar sua abordagem, entendimento do fluxo e capacidade de resolução em tempo real.</strong></span>


**Boa sorte! 🚀**

---
