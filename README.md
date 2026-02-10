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
│   ├── questao1.1/
│   │   ├── RESPOSTA_TEORICA.md
│   │   └── testes/
│   └── questao1.2/
├── parte2-e2e/
├── parte3-frontend/
├── parte4-arquivos/
├── parte5-mobile/
├── parte6-piramide/
└── parte7-mocks/
```

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

## Questão 1.1 - Rate Limiting

### 📖 Contexto
Você precisa testar uma API REST que possui rate limiting de 100 requisições por minuto.

### 💭 Perguntas Teóricas

**1.1.a)** Como você estruturaria seus testes automatizados para validar que o rate limiting está funcionando corretamente?

**1.1.b)** Como você testaria o comportamento da API quando o limite é excedido?

### 🔨 Teste Prático

**API a ser utilizada:** GitHub API - https://api.github.com

A GitHub API tem rate limiting de:
- 60 requisições/hora (sem autenticação)
- 5000 requisições/hora (com autenticação)

**Implemente:**

1. Um teste que valida os headers de rate limiting (`X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`)
2. Um mecanismo que previne seus testes de serem bloqueados
3. Um teste que detecta quando o rate limit foi atingido (status 403)

**Endpoint para testar:**
```
GET https://api.github.com/users/github
```

**Entregáveis:**
- `parte1-api/questao1.1/RESPOSTA_TEORICA.md` - Suas respostas teóricas
- `parte1-api/questao1.1/testes/rate-limiting.spec.js` - Testes implementados
- `parte1-api/questao1.1/testes/utils/rate-limit-helper.js` - Helper de gerenciamento


---

## Questão 1.2 - Gerenciamento de Tokens

### 📖 Contexto
Uma API retorna um token JWT que expira em 15 minutos. Seus testes demoram 45 minutos para executar e fazem múltiplas chamadas autenticadas.

### 💭 Perguntas Teóricas

**1.2.a)** Como você implementaria um mecanismo de refresh token automático?

**1.2.b)** Como você garantiria que testes executados em paralelo não conflitem no gerenciamento de tokens?

### 🔨 Teste Prático

**API a ser utilizada:** ReqRes API - https://reqres.in

**Implemente:**

1. Um sistema de autenticação que obtém token via POST /api/login
2. Um mecanismo que detecta quando o token está prestes a expirar (simule expiração de 2 minutos)
3. Refresh automático do token
4. Testes que executam em paralelo sem conflito de tokens

**Endpoints:**
```javascript
// Login
POST https://reqres.in/api/login
Body: { "email": "eve.holt@reqres.in", "password": "cityslicka" }
Response: { "token": "QpwL5tke4Pnpja7X4" }

// Requisição autenticada (qualquer endpoint GET)
GET https://reqres.in/api/users/2
Headers: { "Authorization": "Bearer {token}" }
```

**Entregáveis:**
- `parte1-api/questao1.2/RESPOSTA_TEORICA.md`
- `parte1-api/questao1.2/testes/auth-manager.js` - Classe de gerenciamento de token
- `parte1-api/questao1.2/testes/token-refresh.spec.js` - Testes implementados


**Dica:** Simule a expiração alterando o tempo de vida do token para 2 minutos no seu código.

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

## Questão 2.2 - Navegação Multi-Abas

### 📖 Contexto
Sistema com múltiplas abas onde:
- Aba 1: Formulário extenso
- Aba 2: Dados calculados (abre ao clicar "Próximo")
- Aba 3: Modal de upload (abre dentro da Aba 2)

**Problema:** Se houver refresh, os dados da Aba 1 são perdidos.

### 💭 Perguntas Teóricas

**2.2.a)** Qual estratégia você usaria para manter referência entre as abas?

**2.2.b)** Como você garantiria que os dados não se percam durante a execução?

**2.2.c)** Como você lidaria com popups/modais que abrem em novas janelas?

### 🔨 Teste Prático

**Site a ser utilizado:** https://demoqa.com/browser-windows

**Implemente:**

1. Teste que abre nova aba via "New Tab"
2. Navega para a nova aba
3. Valida conteúdo da nova aba
4. Retorna para aba original
5. Abre nova janela via "New Window"
6. Gerencia múltiplas janelas simultaneamente

**Entregáveis:**
- `parte2-e2e/questao2.2/RESPOSTA_TEORICA.md`
- `parte2-e2e/questao2.2/testes/multi-tab.spec.js`
- `parte2-e2e/questao2.2/testes/utils/window-manager.js` - Helper de janelas

---

# PARTE 3: TESTES FRONT-END

## Questão 3.1 - Seletores Dinâmicos

### 📖 Contexto
Sistema ExtJS onde todos os IDs são gerados dinamicamente:
- `textfield-1234-inputEl`
- `button-5678-btnEl`
- Os números mudam a cada renderização

### 💭 Perguntas Teóricas

**3.1.a)** Quais estratégias você utilizaria para localizar elementos de forma confiável?

**3.1.b)** Como você lidaria com componentes renderizados condicionalmente?

**3.1.c)** Como identificar 1 botão específico entre 5 botões "Salvar" idênticos?

### 🔨 Teste Prático

**Site a ser utilizado:** https://the-internet.herokuapp.com/dynamic_content

Este site recarrega conteúdo dinamicamente a cada refresh.

**Implemente:**

1. **5 estratégias diferentes** de seleção de elementos:
   - Por texto visível
   - Por estrutura DOM (nth-child)
   - Por atributo parcial
   - Por hierarquia (parent > child)
   - Por XPath

2. Testes que funcionem mesmo após múltiplos refreshes

**Entregáveis:**
- `parte3-frontend/questao3.1/RESPOSTA_TEORICA.md`
- `parte3-frontend/questao3.1/testes/dynamic-selectors.spec.js`
- `parte3-frontend/questao3.1/testes/pages/dynamic-page.js` - Page Object com diferentes estratégias

---


# PARTE 4: TESTES COM ARQUIVOS

## Questão 4.1 - Importação de CSV

### 📖 Contexto
Sistema que importa arquivos CSV com 1000+ linhas e valida:
- Formato dos dados
- Regras de negócio
- Duplicatas
- Relacionamentos

### 💭 Perguntas Teóricas

**4.1.a)** Como validaria que todas as 1000 linhas foram processadas corretamente?

**4.1.b)** Como testaria cenários de erro (arquivo corrompido, dados inválidos)?

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
- `parte4-arquivos/questao4.1/RESPOSTA_TEORICA.md`
- `parte4-arquivos/questao4.1/testes/csv-upload.spec.js`
- `parte4-arquivos/questao4.1/testes/utils/csv-generator.js` - Gerador de CSV
- `parte4-arquivos/questao4.1/testes/fixtures/` - Exemplos de CSV (válido, inválido, corrompido)


**Exemplo de CSV a ser gerado:**
```csv
nome,email,idade,cidade
João Silva,joao@email.com,30,São Paulo
Maria Santos,maria@email.com,25,Rio de Janeiro
```

---

# PARTE 5: TESTES MOBILE

## Questão 5.1 - Automação Mobile

### 📖 Contexto
Aplicativo mobile (iOS e Android) que usa:
- Geolocalização
- Câmera
- Notificações push
- Storage offline
- Sincronização

### 💭 Perguntas Teóricas

**5.1.a)** Qual ferramenta você escolheria e por quê? (Appium, Detox, Maestro, etc.)

**5.1.b)** Como você mockaria geolocalização em testes automatizados?

**5.1.c)** Estratégia para executar mesmos testes em iOS e Android?

### 🔨 Teste Prático

**Aplicativo:** Você pode usar qualquer ferramenta, apenas detalhe como foi feita a instalação e como devem ser executados os testes


**Implemente:**

1. Configuração de ambiente mobile (Appium, Detox e etc )
2. Teste básico de navegação
3. Mock de geolocalização (se possível)
4. Documentação de setup

**Entregáveis:**
- `parte5-mobile/questao5.1/RESPOSTA_TEORICA.md`
- `parte5-mobile/questao5.1/SETUP.md` - Instruções de configuração
- `parte5-mobile/questao5.1/testes/mobile-basic.spec.js` 

---

# PARTE 6: E2E vs TESTES DE COMPONENTES

## Questão 6.1 - Pirâmide de Testes

### 💭 Perguntas Teóricas

**6.1.a)** Explique a diferença entre testes E2E e testes de componentes.

**6.1.b)** Quando usar cada tipo?

### 🔨 Teste Prático

**Site a ser utilizado:** https://demoqa.com/automation-practice-form

**Implemente:**

1. **Teste de Componente (isolado):**
   - Validação de campo de email
   - Validação de campo de telefone
   - Validação de seleção de data
   
2. **Teste E2E (fluxo completo):**
   - Preencher formulário completo
   - Submeter
   - Validar modal de confirmação

**Entregáveis:**
- `parte6-piramide/questao6.1/RESPOSTA_TEORICA.md`
- `parte6-piramide/questao6.1/testes/component.spec.js` - Testes de componente
- `parte6-piramide/questao6.1/testes/e2e.spec.js` - Teste E2E
- `parte6-piramide/questao6.1/JUSTIFICATIVA.md` - Por que cada abordagem foi escolhida

---

# PARTE 7: MOCKS E INTEGRAÇÕES

## Questão 7.1 - Mocks de APIs Externas

### 📖 Contexto
Seu sistema integra com marketplaces (Mercado Livre, Amazon) via API para:
- Publicar produtos
- Atualizar preços
- Processar pedidos
- Atualizar estoque

### 💭 Perguntas Teóricas

**7.1.a)** Como você testaria essas integrações sem afetar os ambientes reais?

**7.1.b)** Como implementaria uma estratégia de mock para simular respostas?

### 🔨 Teste Prático

**API a ser utilizada:** https://fakestoreapi.com (API pública para simular e-commerce)

**Implemente:**

1. **Mock Server** usando MSW, JSON Server ou similar:
   ```javascript
   GET  /products       // Listar produtos
   POST /products       // Criar produto
   PUT  /products/:id   // Atualizar produto
   DELETE /products/:id // Deletar produto
   ```

2. **Testes com mock:**
   - Requisição bem-sucedida
   - Timeout simulado
   - Erro 500 simulado
   - Rate limiting simulado
   - Validação de payload (schema validation)

**Entregáveis:**
- `parte7-mocks/questao7.1/RESPOSTA_TEORICA.md`
- `parte7-mocks/questao7.1/mocks/api-mock.js` - Mock server
- `parte7-mocks/questao7.1/schemas/product-schema.json` - Schema de validação
- `parte7-mocks/questao7.1/testes/with-mock.spec.js` - Testes com mock


**Exemplo de mock esperado:**
```javascript
// Sucesso
GET /products/1 → 200 { id: 1, title: "Product", price: 100 }

// Erro
GET /products/999 → 404 { error: "Product not found" }

// Timeout
GET /products?slow=true → timeout após 5s

// Rate limit
GET /products (após 10 requisições) → 429 { error: "Rate limit exceeded" }
```

---


## O que será avaliado em cada teste

### Respostas Teóricas 
- Clareza e objetividade
- Profundidade técnica
- Exemplos práticos
- Conhecimento de boas práticas

### Código
- ✅ Testes executam sem erro
- ✅ Código limpo e organizado
- ✅ Uso de Page Objects / Helpers
- ✅ Tratamento de erros
- ✅ Comentários em código complexo
- ✅ README com instruções claras
- ✅ Boas práticas de automação
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
# etc...
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
- DemoQA: https://demoqa.com/
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


**Boa sorte! 🚀**

---
