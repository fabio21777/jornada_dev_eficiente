# Refatorando código procedural para OO: classe `PaymentProcessor`

```java
public class PaymentProcessor {

    public void process(List<Installment> installments, Billing billing) {
        for (Installment installment : installments) {
            Payment payment = new Payment(installment.getAmount());
            billing.addPayment(payment); // delega a lógica para o objeto Billing
        }
    }
}
```

1. **Vazamento de encapsulamento:**
   O ponto de refatoração aqui é que o método `process` adicionava pagamentos diretamente na lista interna de `billing`, o que pode ocasionar mudanças de estado indesejadas. O ideal é que a lógica de adicionar o pagamento seja feita dentro do objeto `Billing`, permitindo validações e controle de estado.

2. **Lista e get apenas se necessário:**
   Elementos como listas devem ser modificados apenas por métodos do próprio objeto. É possível usar `unmodifiableList` para evitar que a lista seja modificada fora do objeto `Billing`. O ideal é que o objeto `Billing` tenha um método `addPayment` para adicionar pagamentos, evitando que a lista seja modificada diretamente.
