# Teste Estruturado

Técnica que utiliza a estrutura do código para guiar os testes. Baseia-se em identificar caminhos lógicos e condições de decisão do próprio código para derivar casos de teste. Usamos nossos fluxos, como estruturas condicionais, laços e blocos de código.

O curso irá focar em testes unitários, sem priorizar a cobertura de linhas de código. A indústria normalmente utiliza cerca de 90% de cobertura de linhas de código. Apesar desse número exercitar bem o código e cobrir a maioria dos fluxos, podemos acabar exercitando o código de forma desnecessária, como métodos get e set, que não são necessários para o teste unitário.

## Structural testing: Cobertura por branches

Libs como o JaCoCo testam a cobertura verificando se a branch foi executada, ou seja, se o código foi exercitado. Por exemplo, se temos um `if` com condições mais complexas, uma única execução pode considerar que existe cobertura, mas na verdade não exercitamos todas as possibilidades do `if`. Por isso, é importante exercitar o código de forma que todas as branches sejam testadas.


## Cobertura por branch + condicional

durante o jornada dev, vamos explorar o conceito de cobertura por branch e condicional. A ideia é que, ao escrevermos testes, consigamos exercitar todas as branches do código, garantindo que todas as condições sejam testadas.


## Structural testing: Cobertura por todos os caminhos e MC/DC

A cobertura por todos os caminhos e MC/DC (Modified Condition/Decision Coverage) é uma técnica avançada de teste estrutural que garante que todas as combinações possíveis de condições e decisões sejam testadas. Exite uma forma emperica que é a seguinte:

Para cada condição o numero de testes necesarios e n + 1, onde n é o número de condições. Por exemplo, se temos uma condição com 3 possibilidades (A, B e C), precisamos de 4 testes para cobrir todas as combinações possíveis.

A regra para seleção dos caso é o seguinte:

pegar


```java

public bolean valorEntre(BigDecimal minimo, BigDecimal maximo){

	/**
	 *   A B
	 *1. T T
	 *2. T F
	 *3. F T
	 *4. F F
	 *
	 *
	 */

	bolean valorMaiorQueMinimo = valorEmprestimo.compareTo(minimo) > 0;
	bolean valorMenorQueMaximo = valorEmprestimo.compareTo(maximo) < 0;
	return valorMaiorQueMinimo && valorMenorQueMaximo;
}

Para A, com duas condições, verificamos o caso em que invertemos o valor de A e mantemos B, e o fluxo de execução é alterado.

O caso 3 contempla o teste para A, pois alternamos A para falso e mantemos B como verdadeiro, e assim por diante.

Para B, o caso 2 contempla o cenário em que A é verdadeiro e B é falso. Então, para esse cenário, os casos escolhidos seriam:

1 - A verdadeiro, B verdadeiro
2 - A verdadeiro, B falso
3 - A falso, B verdadeiro

Mais um exemplo:

```java
/**
 * A B C
 * 1. T T T
 * 2. T T F
 * 3. T F T
 * 4. T F F
 * 5. F T T
 * 6. F T F
 * 7. F F T
 * 8. F F F
 */
public boolean tresCondicoes(boolean a, boolean b, boolean c) {
    return a && b && c;
}
```

Seguindo a mesma lógica, teríamos os seguintes casos de teste:

1 - A verdadeiro, B verdadeiro, C verdadeiro
5 - A falso, B verdadeiro, C verdadeiro (cenário para caso A)
3 - A verdadeiro, B falso, C verdadeiro (cenário para caso B)
2 - A verdadeiro, B verdadeiro, C falso (cenário para caso C)

Esses são os casos que garantem a cobertura de todas as combinações possíveis de condições e decisões.

