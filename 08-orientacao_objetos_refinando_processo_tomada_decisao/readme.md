# Orientação a Objetos: Refinando seu Processo de Tomada de Decisão

## O que é algoritmo (Determinístico)

Um algoritmo é uma sequência finita de passos bem definidos e ordenados que visa resolver um problema ou realizar uma tarefa específica.

## O que é heurística

Heurística é uma abordagem prática e não exata para resolver problemas, que utiliza regras empíricas ou experiências passadas para encontrar soluções rápidas e eficientes, mesmo que não garantam a melhor solução possível.

## Heurísticas básicas

1. Anotar classes de domínio como entidades.
2. Criar controllers para aplicações e APIs.
3. Utilizar DTOs para transferir dados entre camadas.
4. Criar classes de caso de uso, como os serviços de negócio.
5. Criar repositórios para abstrair o acesso a dados.

## Heurística de coesão básica

Priorize que a própria classe manipule seus dados, validações e regras de negócio, tornando a classe mais coesa, independente e testável. Mantenha as operações próximas da origem dos dados, evitando a necessidade de passar dados entre várias classes ou métodos.

---

### Exemplo com pouca coesão

```java
public class User {
    private String name;
    private String email;
    private List<String> permissions;

    // Nenhuma validação ou lógica de negócio aqui
}

public class UserService {
    public void save(User user) {
        // Validação e persistência feitas fora da classe User
    }

    public void sendEmail(User user) {
        // Envio de email feito fora da classe User
    }
}
```

No exemplo acima, a lógica de validação, persistência e envio de email está espalhada em outras classes, tornando o código menos coeso, mais difícil de manter e testar.

---

### Exemplo com mais coesão

```java
public class User {
    private String name;
    private String email;
    private List<String> permissions;

    private void validate() {
        // lógica de validação
    }

    private void persist() {
        // lógica de persistência
    }

    public void sendEmail() {
        // lógica de envio de email
    }

    public boolean isAdmin() {
        return permissions.contains("admin");
    }
}
```

---

## Heurística: Quando o tipo padrão não é mais suficiente

Esse é um cenário em que o tipo primitivo ou wrapper não é mais suficiente para representar o domínio do problema. Nesses casos, é necessário criar uma classe específica para encapsular a lógica e as regras de negócio relacionadas ao tipo. Por exemplo, uma classe `PhoneNumber` para representar números de telefone, em vez de usar apenas uma `String`.

```java
public class PhoneNumber {
    private String number;
    private CountryCode countryCode;
    private Format format;

    public PhoneNumber(String number, CountryCode countryCode, Format format) {
        this.number = number;
        this.countryCode = countryCode;
        this.format = format;
        validate();
    }

    private void validate() {
        if (number == null || number.isBlank()) {
            throw new IllegalArgumentException("Número não pode ser vazio");
        }
        if (countryCode == null) {
            throw new IllegalArgumentException("Código do país é obrigatório");
        }
        // Adicione outras validações conforme necessário
    }

    // Métodos de negócio relacionados ao telefone podem ser adicionados aqui
}
```

Ao encapsular regras e validações dentro de uma classe específica, você torna o código mais expressivo, seguro e fácil de manter, além de evitar a propagação de lógica de validação por todo o sistema.

---

### Value objects

Objetos de valor são informações que podem ser criadas e manipuladas como objetos, com atributos e métodos concisos e claros, evitando a necessidade de passar dados entre várias classes ou métodos. Eles são usados para representar conceitos do domínio de forma mais rica e expressiva.

### Tiny objects

Tiny objects são objetos pequenos e simples que encapsulam um único valor ou conceito, como um número de telefone, um endereço de e-mail ou uma data. Eles são usados para evitar o uso de tipos primitivos ou wrappers diretamente, proporcionando uma melhor abstração e encapsulamento.

---

## Heurística: Polimorfismo para postergar decisões ou expressar incertezas no código

Para postergar decisões ou expressar incertezas no código, você pode usar o polimorfismo para criar uma interface que define um contrato para diferentes implementações. Isso permite adiar a decisão de qual implementação usar até o momento em que for realmente necessário, tornando o código mais flexível e extensível. Por exemplo, enviar uma notificação via diferentes canais:

```java
public interface NotificationService {
    void sendNotification(String message);
}

public class EmailNotificationService implements NotificationService {
    @Override
    public void sendNotification(String message) {
        // Lógica para enviar notificação por email
    }
}

public class SmsNotificationService implements NotificationService {
    @Override
    public void sendNotification(String message) {
        // Lógica para enviar notificação por SMS
    }
}

public class NotificationManager {
    private final NotificationService notificationService;

    public NotificationManager(NotificationService notificationService) {
        this.notificationService = notificationService;
    }

    public void notifyUser(String message) {
        notificationService.sendNotification(message);
    }
}

public class Main {
    public static void main(String[] args) {
        NotificationService emailService = new EmailNotificationService();
        NotificationManager manager = new NotificationManager(emailService);
        manager.notifyUser("Olá, usuário!");

        // Para usar SMS, basta trocar a implementação
        NotificationService smsService = new SmsNotificationService();
        manager = new NotificationManager(smsService);
        manager.notifyUser("Olá, usuário via SMS!");
    }
}
```

---

## Heurística: Até coleções podem ganhar suas próprias abstrações

Você pode criar wrappers ou abstrações para coleções, como listas ou mapas, para encapsular a lógica de manipulação e validação dos dados. Isso ajuda a manter o código mais organizado e coeso, além de facilitar a manutenção e a evolução do sistema.

---

## Heurística: Identificando oportunidades de aplicação de funções com Template Method

O padrão Template Method é uma abordagem que permite definir o esqueleto de um algoritmo em uma classe base, enquanto as subclasses podem fornecer implementações específicas para alguns passos do algoritmo. Isso é útil quando você tem um processo comum, mas com variações em algumas etapas.

---

## Heurística: Enums ricos

Enums no Java são classes especiais que podem ter atributos e métodos, tornando-os mais ricos e expressivos. Eles são usados para representar um conjunto fixo de constantes, como dias da semana, estados de um pedido, etc. Por exemplo, você pode criar um enum que, além do valor, tem uma classe que faz algum tipo de processamento específico:

```java
public enum OrderStatus {
    PENDING("Pendente", new PendingProcessor()),
    SHIPPED("Enviado", new ShippedProcessor()),
    DELIVERED("Entregue", new DeliveredProcessor());

    private final String description;
    private final OrderProcessor processor;

    OrderStatus(String description, OrderProcessor processor) {
        this.description = description;
        this.processor = processor;
    }
}
```

---

## Heurística: Inversão de dependências

A inversão de dependências é um princípio de design que sugere que módulos de alto nível não devem depender de módulos de baixo nível, mas ambos devem depender de abstrações. Isso promove a flexibilidade e a testabilidade do código, permitindo que você substitua implementações concretas por mocks ou stubs durante os testes.


## Acoplamento mental e self testing code

> Self testing code: não confie que os parâmetros estão corretos ou que sua implementação está livre de erros. Valide os dados de entrada e saída com assertivas.

```java
public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        validate(name, email); // Validação dos dados de entrada (self testing code)
        this.name = name;
        this.email = email;
    }

    private void validate(String name, String email) {
        assert name != null && !name.isBlank() : "Nome não pode ser vazio";
        assert email != null && !email.isBlank() : "Email não pode ser vazio";
        // Adicione outras validações conforme necessário
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}
```

> **Acoplamento mental** é o acoplamento que ocorre quando o código depende de suposições ou conhecimentos prévios sobre como outras partes do sistema funcionam.

```java
public class UserService {

    private Set<User> users = new HashSet<>();

    public void addUser(User user) {
        users.add(user); // Aqui estamos assumindo que o usuário já foi validado
    }
}
```

No código acima, o `UserService` depende do conhecimento de que o `User` já foi validado antes de ser adicionado ao conjunto. Isso cria um acoplamento mental, pois o desenvolvedor precisa ter certeza de que a validação foi feita corretamente em outro lugar do código.

Existe ainda um cenário de bug: se a definição de unicidade do usuário for, por exemplo, o username, na implementação do Java o método `add` retorna um booleano indicando se o usuário foi adicionado com sucesso ou não. Ou seja, para dois usuários com o mesmo nome, o segundo usuário não será adicionado ao conjunto. Se o serviço anterior não tratar essa situação, existe um bug no sistema.
