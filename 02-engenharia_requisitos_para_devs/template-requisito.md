## Descricao inicial

A funcionalidade de solicitação de empréstimos deve permitir aos clientes aplicar para diferentes tipos de empréstimos (pessoal, imobiliário, auto) através de um formulário digital detalhado. O formulário deve coletar informações financeiras, propósito do empréstimo, e opções de garantia, com campos validados conforme a política de crédito do banco. O sistema deve integrar uma análise de crédito em tempo real e fornecer ao usuário uma resposta preliminar sobre a aprovação.

## Quem pediu ou é responsável essa ideia?

## Descrição detalhada do entendimento das pessoas que vão pegar este requisito para fazer

```markdown
# Requisito: Solicitação de Empréstimos

A funcionalidade de solicitação de empréstimos permitirá que clientes apliquem para diferentes tipos de empréstimos, incluindo:

- **Empréstimo pessoal**
- **Empréstimo imobiliário**
- **Empréstimo para automóveis**

Esta solicitação será realizada por meio de um **formulário digital detalhado**, que deverá conter os seguintes campos obrigatórios e validados de acordo com a política de crédito do banco:

### 1. Informações Pessoais do Cliente:
   - Nome completo
   - CPF
   - Data de nascimento
   - Endereço completo
   - Telefone de contato
   - E-mail

### 2. Informações Financeiras:
   - Renda mensal (validar se o valor está dentro dos limites aceitáveis para o tipo de empréstimo)
   - Relacionamento com o banco (cliente corrente, novo cliente, histórico de crédito com a instituição)
   - Outras obrigações financeiras (dívidas em andamento, outros empréstimos)

### 3. Propósito do Empréstimo:
   - Campo para selecionar o propósito do empréstimo, por exemplo: "Renovação de casa", "Compra de veículo", "Consolidação de dívidas", etc.
   - Campo de texto livre para uma descrição adicional, caso necessário.

### 4. Opções de Garantia (aplicável apenas para certos tipos de empréstimos como imobiliário e auto):
   - Tipo de garantia (imóvel, veículo, etc.)
   - Valor estimado da garantia
   - Detalhes da garantia (placa do veículo, número de registro do imóvel, etc.)
   - Documentação associada (upload de documentos será necessário)

### 5. Detalhes do Empréstimo:
   - Valor solicitado (validar se o valor é elegível para o tipo de empréstimo escolhido)
   - Número de parcelas (de acordo com as opções permitidas pela instituição)
   - Taxa de juros aplicável (calcular conforme tipo de empréstimo e perfil do cliente)

### 6. Validações do Formulário:
   - Todos os campos obrigatórios devem estar preenchidos para submissão.
   - Regras de validação específicas para cada campo conforme a política interna de crédito, como:
     - Verificar formato de CPF e e-mail
     - Validar faixa de renda mínima e máxima permitida para o tipo de empréstimo
     - Garantir que os valores de garantia estejam dentro dos limites aceitos
     - Aplicar regras de crédito específicas da instituição, como limite de endividamento do cliente (exemplo: renda comprometida não pode ser superior a 30%).

### Integração com Sistema de Análise de Crédito:

O sistema deve se integrar ao motor de análise de crédito em **tempo real**, que:
- Consulta o histórico de crédito do cliente nos bureaus de crédito (por exemplo, Serasa, SPC, etc.).
- Avalia o risco de crédito do cliente com base nos dados financeiros e histórico bancário.
- Retorna uma **resposta preliminar** ao usuário sobre a aprovação ou recusa do empréstimo, levando em conta critérios de risco (exemplo: nível de endividamento, garantias oferecidas, pontuação de crédito).

Essa resposta preliminar será exibida na tela ao final da submissão do formulário, indicando:
- **Aprovação preliminar**: Se o cliente for elegível para o empréstimo, informando o valor e as condições sugeridas.
- **Recusa preliminar**: Caso o cliente não atenda aos requisitos iniciais, com uma mensagem explicativa, se possível (por exemplo, "renda insuficiente" ou "garantia abaixo do valor mínimo").

### Requisitos Técnicos:
- O formulário deve ser responsivo e acessível tanto via desktop quanto mobile.
- A integração com o motor de análise de crédito deve garantir uma latência máxima de resposta de 5 segundos.
- Todo o tráfego de dados deve ser protegido com **SSL** e estar em conformidade com as regulamentações de proteção de dados (LGPD).
- As tentativas de submissão do formulário devem ser registradas no sistema de logs para auditoria e rastreamento.

### Cenários de Teste:
- Verificar se o formulário rejeita dados inválidos (CPF incorreto, renda fora dos limites, garantia insuficiente).
- Simular diferentes respostas do motor de análise de crédito (aprovado, recusado, pendente).
- Testar diferentes combinações de tipos de empréstimos e garantias, validando o correto comportamento para cada cenário.

```
### O nosso entendimento foi validado?

## Rascunhos que materializam nosso entendimento do que precisa ser feito

![fluxo-emprestimo drawio](https://gist.github.com/user-attachments/assets/2ab1fcb8-73c5-47d7-bd8b-6087377f3897)

### Os rascunhos foram validados?

Sim

## Especificações dos cenários de testes

```gherkin
Funcionalidade: Solicitação de Empréstimos

  Contexto:
    Dado que o usuário está autenticado no sistema
    E está na página de solicitação de empréstimos

  Cenário: Submissão de um formulário de empréstimo pessoal válido
    Dado que o usuário seleciona "Empréstimo pessoal"
    E preenche todos os campos obrigatórios corretamente
      | nome           | cpf         | data_nasc  | endereço         | telefone     | email               |
      | João Silva     | 123.456.789-09 | 01/01/1980 | Rua A, 123, SP | 11999999999 | joao.silva@email.com |
    E seleciona "Renovação de casa" como propósito do empréstimo
    E insere uma descrição adicional "Renovação completa da cozinha"
    E submete o formulário
    Então uma requisição de análise de crédito é enviada ao sistema
    E uma aprovação preliminar é recebida com os detalhes do empréstimo

  Cenário: Tentativa de submissão com CPF inválido
    Dado que o usuário seleciona "Empréstimo imobiliário"
    E preenche o campo CPF com "123.456.789-00"
    E tenta submeter o formulário
    Então uma mensagem de erro "CPF inválido" é exibida

  Cenário: Submissão com renda mensal fora dos limites para empréstimo imobiliário
    Dado que o usuário seleciona "Empréstimo imobiliário"
    E preenche o campo de renda mensal com "R$ 2000"
    E tenta submeter o formulário
    Então uma mensagem de erro "Renda mensal abaixo do mínimo requerido para empréstimo imobiliário" é exibida

  Cenário: Submissão com garantia insuficiente
    Dado que o usuário seleciona "Empréstimo para automóveis"
    E preenche o campo valor da garantia com "R$ 15000"
    E tenta submeter o formulário
    Então uma mensagem de erro "Valor da garantia abaixo do mínimo requerido para empréstimo de automóveis" é exibida

  Cenário: Simulação de resposta pendente do sistema de análise de crédito
    Dado que o usuário preenche um formulário de empréstimo válido
    Quando o sistema de análise de crédito retorna uma resposta de "pendência de documentação adicional"
    Então uma mensagem de "Pendência: enviar documentação adicional" é exibida na tela

  Cenário: Verificação da conformidade de dados protegidos durante a submissão
    Dado que o usuário preenche um formulário de empréstimo válido
    Quando submete o formulário
    Então a transmissão de dados é realizada via conexão segura (SSL)

```

### Estes cenários foram validados?

Sim

## Histórias/Tarefas que foram derivadas para que seja possível implementar o requisito

## Lista de passo a passo para implementação de cada história