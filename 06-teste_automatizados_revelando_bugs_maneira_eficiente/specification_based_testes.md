# Testes Baseados em Especificação

## Instruções para Criação de Testes

• Identifique os parâmetros ou entradas do programa. Por exemplo, os parâmetros que suas classes e métodos recebem.

• Derive características de cada parâmetro. Por exemplo, um ano (int) deve ser um número inteiro positivo entre 0 e infinito.

  ◦ Algumas dessas características podem ser encontradas diretamente na especificação do programa.

  ◦ Outras podem não ser encontradas nas especificações. Por exemplo, uma entrada não pode ser nula se o método não trata isso adequadamente.

• Adicione restrições para minimizar a suíte de testes.

  ◦ Identifique combinações inválidas. Para algumas características, pode não ser possível combiná-las com outras características.

  ◦ Comportamento excepcional nem sempre precisa ser combinado com todos os valores das outras entradas. Por exemplo, tentar uma única entrada nula pode ser suficiente para testar esse caso específico.

• Gere combinações dos valores de entrada. Estes são os casos de teste.

## Necessidades

Dado o id de um restaurante e o id do usuário, precisamos retornar as formas de pagamento que o usuário em questão aceita e que também são permitidas pelo restaurante.

O retorno esperado é o seguinte:

* descrição da forma de pagamento
* id da forma de pagamento

## Restrições

* id do restaurante é obrigatório
* id do usuário é obrigatório

## Resultado esperado
* formas de pagamento disponíveis

## Testes baseados na especificação (visa, master, elo, máquina de cartão, dinheiro, paypal)

* id usuário, id restaurante
* Usuário, Restaurante
* Combinação
  * usuário visa,master e restaurante aceita visa,master
  * usuário visa,master e restaurante aceita visa
  * usuário visa,master e restaurante aceita elo

## Boundary Testing (Teste de Fronteira)

Técnica que combina **particionamento de equivalência** com **teste de limites**.

**Processo:**

1. **Particione** os dados em classes equivalentes (válidas e inválidas).
2. **Teste as fronteiras** entre essas partições.

**Exemplo - Campo idade (18-65):**

**Partições:**

- Inválida: < 18
- Válida: 18-65
- Inválida: > 65

**Valores de fronteira testados:**

- 17, 18, 19 (fronteira inferior)
- 64, 65, 66 (fronteira superior)

**Por que funciona:**

- O particionamento reduz o número de casos de teste (valores equivalentes têm o mesmo comportamento).
- Testar as fronteiras captura a maioria dos bugs (erros de operadores `<`, `<=`, etc.).

**Resultado:** Máxima cobertura de defeitos com o mínimo de casos de teste.

[Boundary Testing - exemplo](boundary_testing_exemplo.md)

## Structured Testing (Teste Estruturado)

Técnica que utiliza a estrutura do código para guiar os testes. Baseia-se em identificar caminhos lógicos e condições de decisão do próprio código para derivar casos de teste. Usamos nossos fluxos, como estruturas condicionais, laços e blocos de código.

[Structured Testing](structured_testing.md)
