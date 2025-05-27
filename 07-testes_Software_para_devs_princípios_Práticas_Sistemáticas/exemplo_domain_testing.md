# Exemplo de Teste Baseado em Especificação

**Método:** `intersection` (lib common do Java)

Este método recebe duas listas de inteiros positivos e retorna uma nova lista contendo os elementos que estão presentes em ambas as listas.

**Entradas:**
- lista1: [1, 2, 3, 4]
- lista2: [3, 4, 5, 6]

**Saída esperada:** A saída esperada é uma lista contendo os elementos que estão presentes em ambas as listas:
- [3, 4]

## Aplicando a Técnica de Teste Baseado em Especificação

### 1. Olhe para cada entrada de maneira separada

Esses requisitos contam tanto para lista1 quanto para lista2:

- **lista1: [1, 2, 3, 4]**
  - null
  - 0 elementos (vazia)
  - 1 elemento
  - Múltiplos elementos

### 2. Olhe para como elas interagem

As listas podem ter interações, como por exemplo:

1. Têm elementos exatos (1 elemento cada)
2. Têm múltiplos elementos
3. Não têm elementos
4. Têm elementos repetidos

### 3. Regras de domínio

Existem regras de domínio que devem ser consideradas:

1. Se for enviada uma lista nula, o que deve ser feito?
2. Se for enviada uma lista vazia, o que deve ser feito?
3. Se for enviada uma lista com elementos repetidos, o que deve ser feito?
4. null será um resultado válido?
5. Há algum limite de tamanho para as listas?
6. Haverá restrição de tamanho para os elementos das listas?

### 4. Saídas esperadas

1. Lista vazia
2. Lista com elementos
3. Retorna nulo? (isso é requisito)

### 5. Simplifica as possibilidades de teste

1. **Condições guarda:** testar apenas uma vez cada entrada l1 e l2
2. **Condições sem elementos:** lista vazia para l1 e l2
3. **Para apenas 1 elemento:** quando l1 e l2 têm apenas 1 elemento
4. **Condições com múltiplos elementos:** l1 e l2 têm mais de 1 elemento e têm elementos em comum
5. **Condições com múltiplos elementos:** l1 e l2 têm mais de 1 elemento e não têm elementos em comum
6. **Lista l1 ter múltiplos elementos** e lista l2 ter apenas 1 elemento
7. **Lista l2 ter múltiplos elementos** e lista l1 ter apenas 1 elemento
8. **Lista com todos os elementos iguais:** l1 e l2 têm os mesmos elementos

### 6. Crie testes

#### Casos excepcionais

- l1: `null`
- l1: `[]` (lista vazia)
- l2: `null`
- l2: `[]` (lista vazia)

#### Casos com os arrays preenchidos

- l1: `[1]` e l2: `[1]` → lista com 1 elemento em comum
- l1: `[1]` e l2: `[1, 2]` → lista com 1 elemento em comum e outro diferente
- l1: `[1, 2]` e l2: `[1]` → lista com 1 elemento em comum e outro diferente
- l1: `[1, 2]` e l2: `[1, 2]` → lista com 2 elementos em comum
- l1: `[1, 2]` e l2: `[3, 4]` → lista com 2 elementos diferentes
- l1: `[1, 2, 3]` e l2: `[3, 4]` → lista com 1 elemento em comum e outros diferentes
- l1: `[1, 2, 3]` e l2: `[1, 2, 3]` → lista com 3 elementos em comum

## Complexidade de teste

O esforço na construção do teste deve ser feito na parte "complexa" do código, ou seja, onde há mais lógica de negócio. Sempre que possível, desconecte-se do código fonte e faça o exercício desse mini script para derivar os casos de teste.

## Resumo das etapas:

1. **Olhe para cada entrada de maneira separada**
2. **Olhe para como elas interagem**
3. **Regras de domínio**
4. **Saídas esperadas** - Determine os resultados corretos para cada cenário de entrada
5. **Simplifica**
6. **Crie os cenários de teste**
