#[voltar](readme.md)

## Métrica e avaliação de complexidade de código guiada CDD

### Métrica

1. Condicional (condicionais do `if`, loops, if ternário) - 1 ICP
2. Blocos de código adicionais (try, catch, cases do switch, funções como argumento) - 1 ICP
3. Acoplamento com classes específicas do projeto - 1 ICP

### Como avaliar o que foi medido?

* Se é um projeto greenfield, sugiro começar de maneira mais restritiva e avaliar. Limite inicial: 10 ICP.
* Se é um legado com bastante complexidade, aumente esse limite. Limite inicial: 30 ICP. Uma sugestão aqui é começar pelas classes mais complexas e, a partir delas, definir métricas para as classes mais simples. Gradualmente, reduza a complexidade ou evite o aumento da complexidade nas demais classes.

## GuideLine de Teste Automatizado
