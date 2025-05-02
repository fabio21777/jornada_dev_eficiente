# [Voltar](readme.md)

## Guidelines

Criar código de fácil manutenção e fácil evolução deve anteceder qualquer princípio, prática ou design. Essa deve ser uma preocupação central no desenvolvimento de software. Uma forma de alcançar isso é criar guidelines, que são diretrizes que ajudam a orientar o desenvolvimento de software. Essas diretrizes podem incluir práticas recomendadas, padrões de codificação e princípios de design que devem ser seguidos durante o desenvolvimento.

## Guidelines CDD

[CDD](guideLineCdd.md)

## Guidelines de Testes

[Testes](guideLineTeste.md)

## Guidelines de Log

[Log](guideLineLogar.md)

## Guidelines de Coesão

[Coesão](guideLineCoesao.md)

## Guidelines de Generalização e Reuso de Código

[Generalização e Reuso](guideLineGeneralizacao.md)


## Patterns que podem ser utilizados (Sugestões)

1. Controllers 100% coesos (As dependências devem ser usadas por todos os métodos).
2. Services 100% coesos (As dependências devem ser usadas por todos os métodos).
3. Form/Request/DTO como Value Object: o DTO é uma classe e, por isso, pode ter comportamentos. Evite adicionar comportamentos muito complexos, mas é válido incluir métodos que auxiliem no uso do DTO de forma prática e eficiente.
4.
