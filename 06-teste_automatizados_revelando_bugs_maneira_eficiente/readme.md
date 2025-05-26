# Testes automatizados: Revelando bugs de maneira eficiente

Segundo a descrição da aula de introdução, a indústria de software utiliza testes principalmente para validar se o código escrito está funcionando como esperado e, caso não esteja, o teste deve falhar. O olhar acadêmico é diferente: parte da ideia de que, normalmente, o teste deve detectar bugs antes que o software seja entregue ao cliente. Se não detectar bugs, espera-se que haja um QA desenvolvedor.

O curso é voltado para ensinar como escrever testes automatizados e como eles podem ser usados para detectar bugs de maneira eficiente, baseado no livro [Effective Software Testing, by Maurício Aniche](https://www.effective-software-testing.com/).

> Teste reveladores de bugs

O Foco dos teste vai ser encontrar bugs, não será usando tdd


## Pirâmide de testes

1. Testes unitários
2. Testes de integração
3. Testes de sistema
4. Testes de aceitação

![alt text](image-1.png)

> O curso irá focar em testes unitários

## Técnicas de testes

### Specification Based Testing

A ideia dessa técnica de teste é que, a partir de uma especificação, seja possível derivar casos de teste. É uma técnica mais utilizada por QAs, mas também pode ser usada por desenvolvedores para tentar encontrar bugs.

#### [Testes Baseados em Especificação - exemplo](specification_based_testes.md)




## Boundary Testing (Teste de Fronteira)

Técnica que combina **particionamento de equivalência** com **teste de limites**.

**Processo:**

1. **Particione** os dados em classes equivalentes (válidas e inválidas)
2. **Teste as fronteiras** entre essas partições

**Exemplo - Campo idade (18-65):**

**Partições:**

- Inválida: < 18
- Válida: 18-65
- Inválida: > 65

**Valores de fronteira testados:**

- 17, 18, 19 (fronteira inferior)
- 64, 65, 66 (fronteira superior)

**Por quê funciona:**

- Particionar reduz casos de teste (valores equivalentes têm mesmo comportamento)
- Fronteiras capturam a maioria dos bugs (erros de operadores `<`, `<=`, etc.)

**Resultado:** Máxima cobertura de defeitos com mínimo de casos de teste.

[Boundary Testing - exemplo](boundary_testing_exemplo.md)

## Structured Testing (Teste Estruturado)

Técnica que utiliza a estrutura do código para guiar os testes. Baseia-se em identificar caminhos lógicos e condições de decisão do proprio código para derivar casos de teste. Usamos nosso fluxos como estrutras condicionais, laços e blocos de código.


