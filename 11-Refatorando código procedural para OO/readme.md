# Refatorando código procedural para Orientação a Objetos

## [Refatorando classe  `DiscountApplier`](DiscountApplier.md)

## [Refatorando classe `TaxCalculator`](TaxCalculator.md)

## [Refatorando classe `InvoiceGenerator`](InvoiceGenerator.md)

## [Refatorando classe `PaymentProcessor`](PaymentProcessor.md)

## [Refatorando classe `Puzzle`](Puzzle.md)


## Resumo geral

1. use sempre abstrações, como interfaces e classes abstratas e base para refatoração e criação de novas funcionalidades.
2. open closed principle: sempre que for adicionar uma nova funcionalidade, crie uma nova classe que implemente a interface ou herde da classe base, evitando alterar o código existente.
3. O codigo deve depender de abstrações e não de implementações concretas.
4. Encapsulamento: as informações devem ser encapsuladas dentro dos objetos, evitando vazamento de encapsulamento.
