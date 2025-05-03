## [Voltar](./readme.md)

# Cognitive Driven Development (CDD)

CDD é uma abordagem de desenvolvimento que visa criar códigos e encontrar formas de limitar a quantidade de complexidade das unidades de código, definindo um limite de complexidade. Essa abordagem é fortemente inspirada na teoria da carga cognitiva.

## Teoria da carga cognitiva

A teoria da carga cognitiva é um conceito da psicologia educacional que se refere à quantidade de esforço mental que uma pessoa precisa empregar para aprender ou realizar uma tarefa. Essa teoria sugere que a capacidade de processamento cognitivo humano é limitada, e que essa limitação pode afetar a aprendizagem e o desempenho em tarefas complexas.

- **Medida**: A medida é uma regra fixa, geralmente apoiada em um padrão ou convenção.
- **Avaliação**: A avaliação é uma regra subjetiva, que depende do contexto e do conhecimento prévio do avaliador.

## Intrinsic Complex Point (ICP)

O ICP é um ponto de complexidade. São as unidades de complexidade que podem ser medidas e utilizadas para calcular a complexidade de uma unidade de código. O ICP é uma métrica que mede a complexidade intrínseca de um ponto de código, levando em consideração fatores como o número de variáveis, o número de condições e o número de loops. É uma métrica importante para avaliar a qualidade do código.

### Exemplo:

- **if/else, switch/case, for/while**: 1 ICP
- **Acoplamento com classes específicas**: 1 ICP
- **Blocos de código extra (try/catch, finally, funções com argumentos)**: 1 ICP
