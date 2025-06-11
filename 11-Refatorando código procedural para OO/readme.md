# Refatorando código procedural para OO


## Código inicial

```java
package discountapplier;

import common.Basket;

public class DiscountApplier {

    public void apply(Basket basket) {
        boolean ok = discountPerProduct(basket); //1
        if (!ok) discountPerAmount(basket);
    }

    private boolean discountPerProduct(Basket basket) {
        if (basket.has("MACBOOK") && basket.has("IPHONE")) { //2
            basket.subtract(basket.getAmount() * 0.15);
            return true;
        }

        if (basket.has("NOTEBOOK") && basket.has("WINDOWS PHONE")) { //3
            basket.subtract(basket.getAmount() * 0.12);
            return true;
        }

        if (basket.has("XBOX")) {
            basket.subtract(basket.getAmount() * 0.7);
            return true;
        }

        // ... and many more ...

        return false;
    }

    private void discountPerAmount(Basket basket) {

        if (basket.getAmount() <= 1000 && basket.qtyOfItems() <= 2) {
            basket.subtract(basket.getAmount() * 0.02);
            return;
        }

        else if (basket.getAmount() > 3000 && basket.qtyOfItems() < 5 && basket.qtyOfItems() > 2) {
            basket.subtract(basket.getAmount() * 0.05);
            return;
        }

        else if (basket.getAmount() > 3000 && basket.qtyOfItems() >= 5) {
            basket.subtract(basket.getAmount() * 0.06);
            return;
        }
    }
}
```

### Algumas anotações sobre o código

1. Para novos tipos de desconto no método `apply`, seria necessário sempre incrementar o código. Isso não é um problema imediato, mas pode dificultar a manutenção a longo prazo.
2. O uso de valores hardcoded dificulta a manutenção e a adição de novos produtos.
3. O método `subtract` do `Basket` não é uma boa prática, pois não valida as entradas e altera o estado do objeto diretamente, o que pode levar a possíveis erros de lógica e inconsistências no estado do objeto.
4. Lógicas com muitos `ifs` podem crescer e tornar o código muito longo e difícil de ler, o que dificulta a manutenção.
5. O uso de `if` e `else if` pode ser difícil de ler e entender, especialmente quando há muitos casos diferentes a serem considerados, aumentando a chance de erros.
6. É possível (e recomendável) separar a lógica de desconto por produto e por valor, tornando o código mais fácil de ler e entender.
7. A lógica de desconto por produto e por valor pode ser separada em classes diferentes, o que facilita a manutenção, a leitura e a evolução do código.

---

## Refatoração para Orientação a Objetos (criando novas classes)

1. O primeiro passo é separar as lógicas de desconto por produto e por valor em classes distintas, cada uma responsável por um tipo de desconto. Isso facilita a manutenção e a adição de novos tipos de desconto no futuro.
2. Ambas as classes têm as mesmas responsabilidades, mas com lógicas diferentes. Podemos criar uma interface `Discount` que define o método `apply`, e cada classe implementa essa interface com sua lógica específica.
3. A classe `DiscountApplier` agora tem como atributo uma lista de descontos, que são aplicados na ordem em que foram adicionados. Isso permite que novos tipos de desconto sejam adicionados facilmente, sem precisar modificar a classe `DiscountApplier`.

```java
public class DiscountApplier {

    private final List<Discount> discounts; // Lista de descontos a serem aplicados

    public DiscountApplier(List<Discount> discounts) {
        this.discounts = discounts;
    }

    public void apply(Basket basket) {
        discounts.stream()
            .anyMatch(discount -> discount.apply(basket)); // Para ao primeiro true
    }
}






```

```java
public class Main {
    public static void main(String[] args) {
        Basket basket = new Basket(Arrays.asList(new Item("geladeira", 1, 100.0)));
        DiscountApplier discountApplier = new DiscountApplierFactory().build();
        discountApplier.apply(basket);
    }
}
```

### Refatorando as classes de desconto

### class DiscountPerProduct

1. Evite criar interfaces sem necessidade. como por exemplo `Discount` será aplicada apenas uma vez para todas implementações.
2. Utilize o padrão de projeto Strategy para aplicar diferentes lógicas de desconto. Isso permite que você adicione novos tipos de desconto sem modificar o código existente.
3. Evite uso de classes muito com nomes muito concretos, como `DiscountPerProductBasket` para classes que podem ser reutilizadas em diferentes contextos. Use nomes mais genéricos, como `DiscountPerProduct`, para facilitar a reutilização e a manutenção do código.

### class basket

1. A classe `Basket` tem o metodo `subtract`, que altera o estado do objeto diretamente. podemos mudar para um nome mais sugestivo como applyDiscountByPercentage em que o calculo do desconto é feito dentro do método, alem disso adicionaremos uma validação (contract by design) para garantir que o valor do desconto esteja entre 0 e 1 (ou seja, 0% a 100%), oque fazemos dentro do if com  apenas aplicar zero ou lançar uma exceção caso o valor seja inválido, é uma regra de negocio então as duas soluções são válidas.

> Sempre use o javadoc e similares sempre que possivel é uma boa prática para documentar o código e facilitar a compreensão por outros desenvolvedores.

```java

public class Basket {

    private double amount;
    private List<Item> items;

    public Basket(List<Item> itemss) {
        this.items = itemss;
        sumItems();
    }

	....

    /**
     * Aplica desconto baseado em porcentagem.
     * Se a porcentagem de desconto for invalida, nenhum desconto é aplicado.
     *
     * @param discountPercentage porcentagem, [0.0, 1.0]
     */
    public void applyDiscountByPercentage(double discountPercentage) {
        if(discountPercentage < 0 || discountPercentage > 1) {
            //throw new IllegalArgumentException("Invalid discount percentage");
            return;
        }

        this.amount -= this.amount * discountPercentage;
    }

	....

}
```

### Fabrica e dependências do tipo peeer produto

1. Evite aclopar a logica do tipo perr como banco de dados chamadas api, leituras de arquvis, etc. da logica de regras de classses. Isso facilita a manutenção e a reutilização e testes da classe, para isso normalmente usamos o padrão de projeto Factory que é nossa class suja que saber mais sobre  o baixo nivel é passa os dados necessários para a classe de regras de negocio.

```java

public class DiscountApplierFactory {

	private DiscountRepository repository;

	public DiscountApplierFactory(DiscountRepository repository) {
		this.repository = repository;
	}

	public DiscountApplier build() {

		List<DiscountStrategy> discounts = new ArrayList<>();

		List<DiscountProduct> allDiscountsPerProduct = repository.getAllDiscountsPerProduct();

		for (DiscountProduct discountProduct : allDiscountsPerProduct) {
			discounts.add(new DiscountPerProduct(discountProduct.getProducts(), discountProduct.getDiscount()));
		}

		List<DiscountAmount> allDiscountsPerAmount = repository.getAllDiscountsPerAmount();

		for (DiscountAmount discountAmount : allDiscountsPerAmount) {
			discounts.add(new DiscountPerAmount(discountAmount.getMinAmount(), discountAmount.getMaxAmount(),
					discountAmount.getMinItems(), discountAmount.getMaxItems(), discountAmount.getDiscount()));
		}

		return new DiscountApplier(discounts);
	}
}
```

No exemplo acima, a classe `DiscountApplierFactory` é responsável por criar uma instância de `DiscountApplier` com todas as regras de desconto necessárias. Ela busca as regras de desconto em um repositório (que pode ser um banco de dados, arquivo, etc.) e cria as instâncias de `DiscountPerProduct` e `DiscountPerAmount` conforme necessário.


