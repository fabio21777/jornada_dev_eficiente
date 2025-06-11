# Refatorando código procedural para Orientação a Objetos

#### Pontos de melhoria no código procedural

1. Novos tipos de desconto exigem alteração constante no método `apply`, dificultando manutenção.
2. Uso de valores hardcoded dificulta manutenção e adição de novos produtos.
3. O método `subtract` do `Basket` altera o estado diretamente, sem validação.
4. Muitos `ifs` tornam o código longo e difícil de ler.
5. Separar lógica de desconto por produto e por valor facilita manutenção e evolução.

---

## Refatoração para OO

**Passos principais:**
- Separe as lógicas de desconto em classes distintas.
- Use uma interface `Discount` para definir o contrato de desconto.
- Aplique o padrão Strategy para facilitar a adição de novos descontos.
- Utilize uma fábrica (`DiscountApplierFactory`) para montar as dependências.

### Exemplo de implementação

```java
public interface Discount {
    boolean apply(Basket basket);
}

public class DiscountPerProduct implements Discount {
    // lógica de desconto por produto
}

public class DiscountPerAmount implements Discount {
    // lógica de desconto por valor
}

public class DiscountApplier {
    private final List<Discount> discounts;

    public DiscountApplier(List<Discount> discounts) {
        this.discounts = discounts;
    }

    public void apply(Basket basket) {
        discounts.stream().anyMatch(discount -> discount.apply(basket));
    }
}
```

#### Fábrica e dependências do tipo peer

Evite acoplar lógica de infraestrutura (banco, API, arquivos) às regras de negócio. Use uma fábrica para montar as dependências:

```java
public class DiscountApplierFactory {
    private DiscountRepository repository;

    public DiscountApplierFactory(DiscountRepository repository) {
        this.repository = repository;
    }

    public DiscountApplier build() {
        List<Discount> discounts = new ArrayList<>();

        for (DiscountProduct dp : repository.getAllDiscountsPerProduct()) {
            discounts.add(new DiscountPerProduct(dp.getProducts(), dp.getDiscount()));
        }
        for (DiscountAmount da : repository.getAllDiscountsPerAmount()) {
            discounts.add(new DiscountPerAmount(
                da.getMinAmount(), da.getMaxAmount(),
                da.getMinItems(), da.getMaxItems(),
                da.getDiscount()));
        }
        return new DiscountApplier(discounts);
    }
}
```

---

### Melhorando a classe Basket

```java
public class Basket {
    private double amount;
    private List<Item> items;

    // ...

    /**
     * Aplica desconto baseado em porcentagem.
     * @param discountPercentage valor entre 0.0 e 1.0
     */
    public void applyDiscountByPercentage(double discountPercentage) {
        if (discountPercentage < 0 || discountPercentage > 1) {
            return; // ou lance uma exceção, conforme a regra de negócio
        }
        this.amount -= this.amount * discountPercentage;
    }
}
```

---


