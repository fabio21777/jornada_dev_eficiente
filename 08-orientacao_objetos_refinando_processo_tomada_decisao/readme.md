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

## Heurísticas coesão basica

priorize que a propria classe manipule seus dados, validações e regras de negócio,tornando a classe mais coesa e independente e testavel torne as operações proxima da origem dos dados, evitando a necessidade de passar dados entre várias classes ou métodos.

### Exemplo com pouca coesão

```java

/**codigo com pouco coesa */

public class User {
	private String name;
	private String email;
	private List<String> permissions;

	public void save() {
		// lógica de validação e persistência
	}

	public void sendEmail() {
		// lógica de envio de email
	}
}


....

class UserService{

	if(usuario.contains("admin")) {
		// lógica de validação e persistência
	}
}

```

### Exemplo com mais coesão

```java

/**codigo com mais coesa */

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

