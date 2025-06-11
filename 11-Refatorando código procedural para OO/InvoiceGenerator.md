# Refatorando código procedural para OO a class `InvoiceGenerator`

``` java
public class InvoiceGenerator {

    private final EmailSender email;
    private final InvoiceRepository dao;

    public InvoiceGenerator(EmailSender email, InvoiceRepository dao) {
        this.email = email;
        this.dao = dao;
    }

    public Invoice generate(ProvidedService providedService) {

        double amount = providedService.getMonthlyAmount();

        Invoice nf = new Invoice(amount, simpleTax(amount));

        email.sendEmail(nf);
        dao.persist(nf);

        return nf;
    }

    private double simpleTax(double value) {
        return value * 0.06;
    }
}
```

1. Para os métodos `sendEmail` e `persist`, sempre que for adicionando um novo serviço, é necessário alterar o método `generate`, para diconar que o serviço foi adicionado. Isso pode ser resolvido com o padrão Observer, onde a classe `InvoiceGenerator` notifica os serviços que devem ser executados após a geração da nota fiscal.
2. Event bases arquitectures são uma boa solução para esse problema, onde a classe `InvoiceGenerator` dispara um evento(kafka) que é capturado por outros serviços que implementam o evento. Isso permite que novos serviços sejam adicionados sem alterar o código da classe `InvoiceGenerator`.
