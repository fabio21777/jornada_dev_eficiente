# Refatorando código procedural para OO: classe `TaxCalculator`

```java
public class TaxCalculator {

    public double calculateTax(Employee employee) {
        if (DEVELOPER.equals(employee.getRole())) {
            return tenOrTwentyPercent(employee);
        }

        if (DBA.equals(employee.getRole()) || TESTER.equals(employee.getRole())) {
            return fifteenOrTwentyFivePercent(employee);
        }

        // ... outros cargos ...

        throw new RuntimeException("invalid employee");
    }

    private double tenOrTwentyPercent(Employee employee) {
        if (employee.getBaseSalary() > 3000.0) {
            return employee.getBaseSalary() * 0.8;
        } else {
            return employee.getBaseSalary() * 0.9;
        }
    }

    private double fifteenOrTwentyFivePercent(Employee employee) {
        if (employee.getBaseSalary() > 2000.0) {
            return employee.getBaseSalary() * 0.75;
        } else {
            return employee.getBaseSalary() * 0.85;
        }
    }
}
```

---

## Separando os cálculos de impostos em classes separadas

1. Sempre que possível, use o padrão Strategy para criar uma classe para cada cálculo de imposto.
2. As classes de cálculo fazem exatamente a mesma coisa, apenas com valores diferentes. Isso é uma oportunidade para termos apenas uma classe parametrizada com os atributos necessários para realizar o cálculo, deixando o método que usa o cálculo responsável por instanciar a classe com os valores corretos.
3. **Enums ricos:** Podemos usar enums para que cada tipo de cálculo tenha uma classe que implementa a interface de cálculo de imposto. Assim, podemos usar o enum para instanciar a classe correta (funciona melhor para valores fixos; para cenários muito dinâmicos, essa abordagem perde um pouco de valor).
4.  **Resolver** : essa estrategia consiste em criar uma classe que encapsula a regra de instancia do objeto de calculo no fundo é o padrão Factory Method, onde a classe de calculo é instanciada de acordo com a role do funcionário. Isso permite que o código de cálculo seja mais flexível e extensível, pois novas regras de cálculo podem ser adicionadas facilmente sem modificar o código existente.

```java
public class TaxCalculationResolver {

	private TaxStrategiesRepository repository;

	public TaxCalculationResolver(TaxStrategiesRepository repository) {
		this.repository = repository;
	}
	public TaxCalculationStrategy forRole(Role role) {
		TaxValues taxValues = repository.getForRole(role);

		return new ThresholdBasedTaxCalculation(taxValues.getThreshold(),
				taxValues.getAboveTax(),
				taxValues.getBelowTax());
	}
}

```

