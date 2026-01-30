<p align="center">
  <img src="logo-magazord.png" width="220" />
</p>

# Teste para vaga de Analista de Qualidade Sênior – Magazord

Este repositório tem como objetivo avaliar candidatos à vaga de **Analista de Qualidade Sênior** na **Magazord**.

O teste é focado em **qualidade de software**, **testes automatizados**, **arquitetura de testes**, **raciocínio técnico** e **boas práticas** aplicadas a cenários reais.

---

## Instruções Gerais

- Responda às questões de forma **clara, objetiva e bem estruturada**
- Sempre que possível, utilize **exemplos práticos**, **pseudocódigo** ou **código real**
- Não é necessário criar um projeto executável
- Você pode responder diretamente neste repositório (README ou arquivos separados, se desejar)
- Sinta-se à vontade para sugerir melhorias, abordagens alternativas ou boas práticas

---

## Questionário Técnico

### Especialização em Testes Automatizados

---

## PARTE 1: Testes de API

### Questão 1.1 – Rate Limiting

**Cenário:**  
Você precisa testar uma API REST que possui rate limiting de **100 requisições por minuto**.

**Perguntas:**
- Como você validaria que o rate limiting está funcionando corretamente?
- Como garantir que seus testes não sejam bloqueados durante a execução normal?
- Como testar o comportamento da API quando o limite é excedido?

---

### Questão 1.2 – Autenticação com JWT

**Cenário:**  
Uma API retorna um token JWT que expira em **15 minutos**.  
A suíte de testes demora **45 minutos** e realiza múltiplas chamadas autenticadas.

**Perguntas:**
- Descreva sua estratégia para gerenciar autenticação durante toda a execução
- Implemente (em pseudocódigo ou código real) um mecanismo de refresh token automático
- Como garantir que testes em paralelo não conflitem no uso de tokens?

---

### Questão 1.3 – Webhooks Assíncronos

**Cenário:**  
Um endpoint de webhook:
- Recebe dados via `POST`
- Processa de forma assíncrona (5 a 300 segundos)
- Envia callback para uma URL configurada
- Callback contém um hash **HMAC SHA-256**

**Perguntas:**
- Desenhe a arquitetura da solução de testes
- Implemente a validação do hash HMAC
- Como lidar com timeouts variáveis?
- Como isolar testes paralelos?
- Como simular falhas (timeout, URL inválida, erro 500)?

---

## PARTE 2: Testes E2E

### Questão 2.1 – Fluxo de Checkout

**Cenário:**  
Fluxo de checkout com:
- Carrinho
- Cupom de uso único
- Gateway externo (sandbox)
- Confirmação por e-mail
- Atualização de status no banco

**Perguntas:**
- Como garantir cupons únicos por execução?
- Como validar e-mails sem depender de serviços externos?
- Estratégia de rollback/limpeza
- Como lidar com falhas intermitentes do gateway?

---

### Questão 2.2 – Múltiplas Abas e Modais

**Cenário:**  
Sistema com múltiplas abas e modal para upload de documentos.

**Problema:**  
Refresh em qualquer aba perde os dados.

**Perguntas:**
- Estratégia para manter referência entre abas
- Exemplo de navegação automatizada entre as abas
- Como evitar perda de dados?
- Como lidar com novas janelas/modais?
- Abordagem de debug quando falha na Aba 3

---

## PARTE 3: Seletores e Frontend

### Questão 3.1 – ExtJS com IDs Dinâmicos

**Perguntas:**
- Estratégias para localizar elementos de forma confiável
- Implemente 3 seletores diferentes para um botão "Salvar"
- Como lidar com renderização condicional?
- Como diferenciar 5 botões "Salvar" idênticos?

---

### Questão 3.2 – React Avançado

**Cenário:**
- Lazy loading
- Redux
- IDs dinâmicos
- Grids virtualizados

**Perguntas:**
- Como testar uma linha específica em um grid virtualizado?
- Código validando Redux → UI
- Como esperar lazy loading?
- Estratégia para permissões
- Como evitar race conditions?

---

## PARTE 4: Testes com Importação de Arquivos

### Questão 4.1 – CSV com 1000+ linhas

**Perguntas:**
- Estruturação dos dados
- Validação de processamento completo
- Testes de erro (arquivo corrompido, dados inválidos)

---

### Questão 4.2 – Processamento Assíncrono em Massa

**Cenário:**  
Arquivos CSV, XLSX, XML, JSON com até 100.000 registros.

**Perguntas:**
- Arquitetura da suíte de testes
- Geração dinâmica de arquivos
- Validação de retry e processamento parcial
- Testes de performance
- Validação eficiente de relatórios de erro

---

## PARTE 5: Testes Mobile

### Questão 5.1 – Mobile Tradicional

**Perguntas:**
- Ferramenta escolhida e justificativa
- Mock de geolocalização
- Testes offline/online
- Push notifications
- Estratégia multi-plataforma (iOS/Android)

---

### Questão 5.2 – Realidade Aumentada (AR)

**Perguntas:**
- É viável automatizar? Justifique
- Estratégia de testes
- Testes de gestos complexos
- Variabilidade de hardware
- O que automatizar vs. manter manual

---

## PARTE 6: E2E vs Testes de Componentes

### Questão 6.1

**Teórica:**
- Diferença entre E2E e Componentes
- Quando usar cada um
- Vantagens e desvantagens
- Pirâmide de testes

**Prática:**
- Teste de componente para validação de CPF
- Teste E2E para fluxo completo de cadastro
- Justificativa das escolhas

---

## PARTE 7: Mocks e Integrações Externas

### Questão 7.1 – Marketplaces

**Perguntas:**
- Estratégia de testes sem impactar ambientes reais
- Mock da API do Mercado Livre
- Testes de erro
- Validação de payloads

---

### Questão 7.2 – Fluxo Completo de Pedido

**Cenário:**  
E-commerce → Pagamento → WMS → Transportadora → Webhook → E-mail

**Perguntas:**
- Arquitetura de testes
- Mock de cada integração
- Testes ponta a ponta isolados
- Código de mock de webhook
- Como evitar falhas silenciosas após mudanças de API

---

## Envio do Teste

- Suba o repositório no seu GitHub
- Envie o link diretamente ao recrutador
- ❗ Não serão aceitas alterações após o envio

