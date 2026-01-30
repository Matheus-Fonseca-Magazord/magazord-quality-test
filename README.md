<p align="center">
  <img src="logo-magazord.png" width="240" />
</p>

---

# Teste para vaga de Analista de Qualidade Sênior – Magazord

Este repositório tem como objetivo avaliar candidatos à vaga de **Analista de Qualidade Sênior** na **Magazord**.

O teste é focado em **testes automatizados**, **arquitetura de testes**, **estratégia de qualidade**, **integrações** e **boas práticas aplicadas a cenários reais**.

---

## Instruções Gerais

- Responda às questões de forma clara e objetiva  
- Utilize exemplos práticos, pseudocódigo ou código real sempre que julgar necessário  
- Não é obrigatório criar um projeto executável  
- As respostas podem ser adicionadas neste próprio repositório  
- Não serão aceitas alterações após o envio

---

## PARTE 1: Testes API

---

### Questão 1.1

**Cenário:**  
Você precisa testar uma API REST que possui rate limiting de 100 requisições por minuto.

**Pergunta:**  
Como você estruturaria seus testes automatizados para:

- Validar que o rate limiting está funcionando corretamente?
- Garantir que seus testes não sejam bloqueados pelo rate limiting durante a execução normal?
- Testar o comportamento da API quando o limite é excedido?

---

### Questão 1.2

**Cenário:**  
Uma API retorna um token JWT que expira em 15 minutos. Seus testes demoram 45 minutos para executar e fazem múltiplas chamadas autenticadas.

**Pergunta:**

- Descreva sua estratégia para gerenciar a autenticação durante toda a suite de testes
- Implemente (em pseudocódigo ou código real) um mecanismo de refresh token automático
- Como você garantiria que testes executados em paralelo não conflitem no gerenciamento de tokens?

---

### Questão 1.3

**Cenário:**  
Você está testando um endpoint de webhook que:

- Recebe dados via POST
- Processa assincronamente (pode levar de 5 a 300 segundos)
- Envia callback para uma URL configurada quando o processamento termina
- O callback contém um hash HMAC SHA-256 para validação de integridade

**Pergunta:**

- Desenhe a arquitetura completa da solução de testes automatizados
- Implemente o código para validar o hash HMAC recebido
- Como você lidaria com timeouts variáveis?
- Como você isolaria os testes para executá-los em paralelo sem colisões?
- Como você simularia falhas no callback (timeout, URL inválida, resposta 500)?

---

## PARTE 2: TESTES E2E

---

### Questão 2.1

**Cenário:**  
Você precisa testar um fluxo de checkout que envolve:

- Adicionar produtos ao carrinho
- Aplicar cupom de desconto (que só pode ser usado uma vez)
- Processar pagamento com gateway externo (sandbox)
- Receber confirmação por email
- Atualizar status no banco de dados

**Pergunta:**

- Como você garantiria que cada execução de teste use um cupom válido diferente?
- Como você validaria o email de confirmação sem depender de serviços externos não confiáveis?
- Descreva sua estratégia de rollback/limpeza após cada teste
- Como você lidaria com falhas intermitentes do gateway de pagamento?

---

### Questão 2.2

**Cenário:**  
Sistema com múltiplas abas onde:

- Aba 1: Usuário preenche um formulário extenso (20+ campos)
- Ao clicar em "Próximo", abre Aba 2 com dados calculados baseados na Aba 1
- Na Aba 2, usuário pode abrir Aba 3 (modal) para upload de documentos
- Após upload, retorna para Aba 2 e deve clicar em "Finalizar"

**PROBLEMA:**  
Se houver refresh em qualquer aba, os dados da Aba 1 são perdidos e o teste falha

**Pergunta:**

- Qual estratégia você usaria para manter referência entre as abas?
- Implemente código demonstrando como você navegaria entre as 3 abas
- Como você garantiria que os dados não se percam durante a execução?
- Como você lidaria com popups/modais que abrem em novas janelas?
- Qual seria seu approach para debug quando o teste falha na "Aba 3"?

---

## PARTE 3: TESTES FRONT-END

---

### Questão 3.1

**Cenário:**  
Sistema ExtJS onde todos os IDs são gerados dinamicamente no formato:

- textfield-1234-inputEl  
- button-5678-btnEl  
- grid-9012-body  

Os números mudam a cada renderização.

**Pergunta:**

- Quais estratégias você utilizaria para localizar elementos de forma confiável?
- Implemente 3 diferentes seletores para um botão "Salvar" neste cenário
- Como você lidaria com componentes que são renderizados condicionalmente?
- Qual seria sua abordagem se o sistema tivesse 5 botões "Salvar" visualmente idênticos na mesma tela?

---

### Questão 3.2

**Cenário:**  
Aplicação React com:

- Componentes carregados via lazy loading
- State management com Redux
- IDs gerados aleatoriamente
- Elementos que aparecem/desaparecem baseado em permissões do usuário
- Grids virtualizados (renderizam apenas linhas visíveis)

**Pergunta:**

- Como você testaria uma linha específica em um grid com 10.000 registros que usa virtualização?
- Implemente código para validar que uma ação no Redux Store refletiu corretamente na UI
- Como você esperaria elementos que são carregados via lazy loading?
- Descreva uma estratégia para testar componentes que só aparecem para usuários com permissões específicas
- Como você evitaria race conditions em componentes assíncronos?

---

## PARTE 4: TESTES COM ARQUIVOS DE IMPORTAÇÃO

---

### Questão 4.1

**Cenário:**  
Sistema que importa arquivos CSV com 1000+ linhas e valida:

- Formato dos dados
- Regras de negócio complexas
- Duplicatas
- Relacionamentos com dados existentes

**Pergunta:**

- Como você estruturaria os dados de teste (arquivos CSV)?
- Como você validaria que todas as 1000 linhas foram processadas corretamente?
- Como você testaria cenários de erro (arquivo corrompido, dados inválidos)?

---

### Questão 4.2

**Cenário:**  
Sistema que processa múltiplos tipos de arquivo (CSV, XLSX, XML, JSON) e:

- Cada arquivo pode ter até 100.000 registros
- Processamento é assíncrono com fila
- Sistema gera relatório de erros
- Alguns registros podem ser processados parcialmente
- Sistema possui retry automático para falhas temporárias

**Pergunta:**

- Projete uma suite de testes automatizados completa para este cenário
- Como você geraria arquivos de teste de diferentes tamanhos dinamicamente?
- Implemente código para validar processamento parcial e retry
- Como você testaria a performance da importação?
- Como você validaria o relatório de erros sem processar 100.000 linhas em cada teste?

---

## PARTE 5: TESTES MOBILE

---

### Questão 5.1

**Cenário:**  
Aplicativo mobile (iOS e Android) que usa:

- Geolocalização
- Câmera
- Notificações push
- Armazenamento offline
- Sincronização quando volta online

**Pergunta:**

- Qual ferramenta você escolheria e por quê? (Appium, Detox, Maestro, etc.)
- Como você mockaria geolocalização em testes automatizados?
- Como você testaria o comportamento offline/online?
- Como você validaria notificações push?
- Descreva sua estratégia para executar os mesmos testes em iOS e Android

---

### Questão 5.2

**Cenário:**  
App mobile com realidade aumentada (AR) que:

- Usa a câmera para detectar objetos
- Sobrepõe informações 3D
- Requer calibração de sensores
- Funciona offline com sync posterior
- Tem gestos complexos (pinch, rotate, swipe multi-touch)

**Pergunta:**

- É viável automatizar testes para este cenário? Justifique.
- Se sim, qual seria sua abordagem? Se não, quais alternativas você proporia?
- Como você testaria gestos complexos?
- Como você lidaria com a variabilidade de hardware (diferentes câmeras, sensores)?
- Que tipo de testes você automatizaria vs. manteria manuais?

---

## PARTE 6: E2E vs TESTES DE COMPONENTES

---

### Questão 6.1

**Pergunta Teórica:**  
Explique detalhadamente:

- A diferença entre testes E2E e testes de componentes
- Quando usar cada tipo
- Vantagens e desvantagens de cada abordagem
- Como você equilibraria a pirâmide de testes em um projeto real

**Pergunta Prática:**  
Dado um formulário de cadastro com validações complexas (CPF, email, data de nascimento, senha com requisitos, etc.):

- Implemente um teste de componente para a validação de CPF
- Implemente um teste E2E para o fluxo completo de cadastro
- Justifique por que você escolheu testar cada aspecto em cada nível

---

## PARTE 7: MOCKS E INTEGRAÇÕES EXTERNAS

---

### Questão 7.1

**Cenário:**  
Seu sistema integra com marketplaces (Mercado Livre, Amazon, Shopee) via API para:

- Publicar produtos
- Atualizar preços
- Processar pedidos
- Atualizar estoque

**Pergunta:**

- Como você testaria essas integrações sem afetar os ambientes reais dos marketplaces?
- Implemente uma estratégia de mock para simular respostas da API do Mercado Livre
- Como você testaria cenários de erro (timeout, rate limiting, erro 500)?
- Como você validaria que o payload enviado está correto sem fazer requisições reais?

---

### Questão 7.2

**Cenário:**  
Sistema que:

- Recebe pedidos no e-commerce
- Envia para gateway de pagamento (PagSeguro)
- Após confirmação, envia para WMS via API
- WMS confirma separação e envia para transportadora via EDI
- Transportadora retorna código de rastreio via webhook
- Sistema envia email ao cliente com rastreio

**Pergunta:**

- Desenhe uma arquitetura de testes que cubra todo este fluxo
- Como você mockaria cada sistema externo?
- Como você testaria o fluxo completo sem depender de sistemas externos?
- Implemente código para mockar o webhook da transportadora
- Como você garantiria que mudanças nas APIs externas não quebrem seus testes silenciosamente?
- Como você testaria cenários de falha em cada etapa da cadeia?

---

