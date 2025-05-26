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
