# Práticas de Design de Código Para Seu Dia a Dia (OO)

## Direcionamentos

## Qualidade não é negociável

O código deve ser desenvolvido com um design proporcional à complexidade, considerando o conhecimento disponível no momento da produção.

## Aceite: tomamos decisões ruins

Você inevitavelmente deixará decisões ruins pelo caminho, independentemente do seu nível de experiência.

## Fazemos o que foi combinado

A prioridade máxima é funcionar de acordo com o caso de uso.

## Prática

### Implemente de fora para dentro

Execute o seu código o mais rápido possível. Priorize implementar de fora para dentro, dessa forma você visualiza o que realmente precisa e utiliza uma abordagem mais incremental. O "fora" aqui pode ser o endpoint que vai receber uma chamada ou até mesmo um teste automatizado.

```java

public class NovoConviteRequest {
	@NotBlank
	@Email
	private String email;
	@min(1)
	@NotNull
	private Integer diasExpiracao;

	public NovoConviteRequest(String email, int diasExpiracao) {
		this.email = email;
		this.diasExpiracao = diasExpiracao;
	}

	public Convite toModel(Conta conta) {
		return new Convite(this.email, this.diasExpiracao, conta);
	}
}

@RestController
public class GeraNovoConviteController {
    /**
     * - Criar um novo endpoint que vai receber um post
     * - Neste endpoint eu preciso receber a pessoa logada que gerar o convite e também o projeto
     *   daquele convite.
     *      - A pessoa logada vai vir via header
     *      - O projeto pode vir via parametro combinado na própria url (path variable)
     * - Também preciso receber os dados do convite. Email e dias de expiração
     * - Carregar a pessoa logada e verificar se ela existe mesmo (use o getOrThrow e lance RespostaStatusException)
     * - Carregar o projeto e verificar se ele existe mesmo (use o getOrThrow e lance RespostaStatusException)
     * - A pessoa logada precisa ser dona do projeto (lance RespostaStatusException)
     * - Eu crio o novo convite para aquele email com aquela data de expiração
     *      - Crie um método chamado toModel na classe de request
     * - Salvo este convite
     *      - Utilize o EntityManager
     * - Preciso mandar um email para a pessoa que vai receber o convite
     *      - Deixe fake por enquanto
     */

	private final PessoaUsuarioRepository pessoaUsuarioRepository;

	private final ContaRepository contaRepository;

	public GeraNovoConviteController(PessoaUsuarioRepository pessoaUsuarioRepository, ContaRepository contaRepository) {
		this.pessoaUsuarioRepository = pessoaUsuarioRepository;
		this.contaRepository = contaRepository;
	}

	@PostMapping("/api/contas/{idConta}/convites")
	public void exexuta(@PathVariable Long idConta,@RequestHeader("id-pessoa-logada") , @valid @RequestBody NovoConviteRequest request) {
		System.out.println("idConta: " + idConta);
		System.out.println("idPessoaLogada: " + idPessoaLogada);
		System.out.println("NovoConviteRequest: " + request);

		// caregar a pessoa logada
		pessoaLogada pessoa = pessoaUsuarioRepository.findById(idPessoaLogada)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Pessoa não encontrada"));


		//carregar a conta
		Conta conta = contaRepository.findById(idConta)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Conta não encontrada"));

		// verificar se a pessoa logada é dona da conta, tem um metódo que verificar se a pessoa é pertece a pessoa
		if (!conta.perteceAPessoa(pessoa)) {
			throw new RespostaStatusException(HttpStatus.FORBIDDEN, "A pessoa logada não é dona da conta");
		}


		// criar o novo convite
		Convite convite = request.toModel();


		system.out.println("Convite: " + convite);


	}
}

```

### Proteger as bordas do sistema

- Proteja as bordas do sistema, ou seja, valide o que entra e o que sai do sistema. Isso inclui validar os dados de entrada e saída, garantindo que os dados estejam no formato correto e que não haja dados inválidos ou maliciosos.

### Não retorne null

Não retornamos `null` dentro das regras da aplicação. Pense que seu computador vai explodir ao retornar `null`. O retorno `null` quebra o fluxo do método. Se o método espera um retorno, é melhor lançar uma exceção.

```java
// Exemplo usando o Optional
Conta conta = contaRepository.findById(idConta)
        .orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Conta não encontrada"));

// O código que chama o método findById não precisa saber que o retorno pode ser nulo. Ele só vai receber a conta ou uma exceção, não sendo necessário fazer o tratamento de nulo.
private Conta findById(Long id) {
    return Optional.ofNullable(entityManager.find(Conta.class, id))
            .orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Conta não encontrada"));
}
```

### Não ligamos parâmetros de borda externa com entidades

Separamos as bordas externas do sistema do seu núcleo. Não conectamos diretamente os parâmetros de requisição externa com objetos de domínio, assim como não serializamos objetos de domínio para resposta da API. Essa separação ajuda a manter o núcleo do sistema desacoplado e mais seguro.


### Informação obrigatória entra pelo construtor

Usamos o contrutor para criar o objeto no estado valido.Como no exemplo abaixo, o construtor é usado para criar o objeto `NovoConviteRequest` com os dados obrigatórios. Isso garante que o objeto sempre estará em um estado válido quando for criado, sem criar os métodos `set` para cada atributo.

```java
public class NovoConviteRequest {
	@NotBlank
	@Email
	private String email;
	@min(1)
	@NotNull
	private Integer diasExpiracao;

	public NovoConviteRequest(String email, int diasExpiracao) { // Construtor
		this.email = email;
		this.diasExpiracao = diasExpiracao;
	}

	//novo construtor apenas com o email
	public NovoConviteRequest(String email) {
		this.email = email;
	}

	public Convite toModel(Conta conta) {
		return new Convite(this.email, this.diasExpiracao, conta);
	}
}
```

### Deixe pistas quando a compilação não resolver

Deixamos pista que facilitem o suso do código onde não conseguimos resolver na compilação. Isso pode ser feito através de comentários, documentação ou até mesmo criando métodos que ajudem a entender o que está acontecendo. Isso ajuda a manter o código mais legível e fácil de entender para outros desenvolvedores.


```java

public class convite {
	@NotBlank
	@Email
	private String email;
	@min(1)
	@NotNull
	private LocalDate dataExpiracao;

	private Conta conta;

	@Deprecated("usado paenas para o hibernate")
	public Convite() {
		//usando para api no padrão javabean
	}

	/**
	 * o java doc também é uma forma de deixar pistas
	 *  Construtor para criar um convite
	 *
	 * @param email
	 * @param dataExpiracao
	 * @param conta
	 *
	 *  */
	public Convite(String email, @Future localDate dataExpiracao, Conta conta) {
		this.email = email;
		this.dataExpiracao = dataExpiracao;
		this.conta = conta;
	}
	public Convite(String email, int diasExpiracao, Conta conta) {
		this.email = email;
		this.dataExpiracao = LocalDate.now().plusDays(diasExpiracao);
		this.conta = conta;
	}


}


```

### Utilize o que está pronto

Usamos tudo que conhecemos e que já está pronto. Não reinventamos a roda. Isso inclui usar bibliotecas, frameworks e ferramentas que já existem e são confiáveis. Isso ajuda a economizar tempo e esforço, além de garantir que o código esteja mais seguro e testado.Menos código para manter e menos bugs para corrigir. Isso também ajuda a manter o código mais legível e fácil de entender, já que estamos usando soluções conhecidas e testadas.


### Utilizamos cdd

CDD é uma abordagem de desenvolvimento que visa criar códigos e encontrar formas de limitar a quantidade de complexidade das unidades de código, definindo um limite de complexidade. Essa abordagem é fortemente inspirada na teoria da carga cognitiva. A teoria da carga cognitiva é um conceito da psicologia educacional que se refere à quantidade de esforço mental que uma pessoa precisa empregar para aprender ou realizar uma tarefa. Essa teoria sugere que a capacidade de processamento cognitivo humano é limitada, e que essa limitação pode afetar a aprendizagem e o desempenho em tarefas complexas.


```java

/**
 * - Acoplamento com classes específicas do sistema - 1 ICP
 * - condicionais - 1 ICP
 * - blocos extra (try, cases) - 1 ICP
 *
 *  limite = 20
 */

@RestController
public class GeraNovoConviteController {

	//1 ICP
	private final PessoaUsuarioRepository pessoaUsuarioRepository;

	//1 ICP
	private final ContaRepository contaRepository;

	public GeraNovoConviteController(PessoaUsuarioRepository pessoaUsuarioRepository, ContaRepository contaRepository) {
		this.pessoaUsuarioRepository = pessoaUsuarioRepository;
		this.contaRepository = contaRepository;
	}

	@PostMapping("/api/contas/{idConta}/convites")
	public void exexuta(@PathVariable Long idConta,@RequestHeader("id-pessoa-logada") , @valid @RequestBody NovoConviteRequest request) {
		System.out.println("idConta: " + idConta);
		System.out.println("idPessoaLogada: " + idPessoaLogada);
		System.out.println("NovoConviteRequest: " + request);

		// caregar a pessoa logada
		// 1 ICP
		// 1 ICP
		pessoaLogada pessoa = pessoaUsuarioRepository.findById(idPessoaLogada)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Pessoa não encontrada"));


		//carregar a conta
		// 1 ICP
		Conta conta = contaRepository.findById(idConta)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Conta não encontrada"));

		// verificar se a pessoa logada é dona da conta, tem um metódo que verificar se a pessoa é pertece a pessoa
		// 1 ICP
		if (!conta.perteceAPessoa(pessoa)) {
			throw new RespostaStatusException(HttpStatus.FORBIDDEN, "A pessoa logada não é dona da conta");
		}
		// 1 ICP

		// criar o novo convite
		Convite convite = request.toModel();


		system.out.println("Convite: " + convite);


	}
}
```


### Só alteramos referências que criamos


Só alteramos referêmcia que criamos, Não mexemos nos objetos alheios. A não ser que esse objeto seja criado para isso.Eviter alterar referências de outras entidades a partir de uma entidade que não é a dona. Isso ajuda a manter o código mais legível e fácil de entender, além de evitar problemas de concorrência e inconsistência de dados.
```java
public class Convite {
	@NotBlank
	@Email
	private String email;
	@min(1)
	@NotNull
	private LocalDate dataExpiracao;

	private Conta conta;

	@Deprecated("usado paenas para o hibernate")
	public Convite() {
		//usando para api no padrão javabean
	}

	public Convite(String email, @Future localDate dataExpiracao, Conta conta) {
		this.email = email;
		this.dataExpiracao = dataExpiracao;
		this.conta = conta;
	}

	//exemplo de método que altera a referência, evite usar
	public aceitarConvite() {
		this.conta.adicionarMembro(this.email);
	}


	//exemplo corrigindo o problema
	@RestController
public class GeraNovoConviteController {
	private final PessoaUsuarioRepository pessoaUsuarioRepository;

	private final ContaRepository contaRepository;

	public GeraNovoConviteController(PessoaUsuarioRepository pessoaUsuarioRepository, ContaRepository contaRepository) {
		this.pessoaUsuarioRepository = pessoaUsuarioRepository;
		this.contaRepository = contaRepository;
	}

	@PostMapping("/api/contas/{idConta}/convites")
	public void exexuta(@PathVariable Long idConta,@RequestHeader("id-pessoa-logada") , @valid @RequestBody NovoConviteRequest request) {
		System.out.println("idConta: " + idConta);
		System.out.println("idPessoaLogada: " + idPessoaLogada);
		System.out.println("NovoConviteRequest: " + request);

		// caregar a pessoa logada
		pessoaLogada pessoa = pessoaUsuarioRepository.findById(idPessoaLogada)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Pessoa não encontrada"));


		//carregar a conta
		Conta conta = contaRepository.findById(idConta)
			.orElseThrow(() -> new RespostaStatusException(HttpStatus.NOT_FOUND, "Conta não encontrada"));

		// verificar se a pessoa logada é dona da conta, tem um metódo que verificar se a pessoa é pertece a pessoa
		if (!conta.perteceAPessoa(pessoa)) {
			throw new RespostaStatusException(HttpStatus.FORBIDDEN, "A pessoa logada não é dona da conta");
		}


		// criar o novo convite
		Convite convite = request.toModel();

		convite.aceitarConvite();

		// a propria entidade que vai adicionar o membro e alterar a referência
		conta.adicionarMembro(convite.getEmail());


		system.out.println("Convite: " + convite);


	}
}
}
```

### Derive testes de maneira sistemática

Testes automatizados devem ser derivados de maneira pragmática utilizando técnicas já conhecidas. Após cobrir os casos padrão, podemos usar nossa criatividade para extrapolar e testar cenários adicionais, garantindo maior robustez e confiabilidade no sistema.

```java

public class EmployeeBonus {
    public double calculateBonus(double salary, int yearsWorked, boolean hasMetTarget) {
        if (yearsWorked > 10 && hasMetTarget) {
            return salary * 0.15; // 15% bonus
        } else if (yearsWorked > 5 && hasMetTarget) {
            return salary * 0.10; // 10% bonus
        } else if (yearsWorked > 5 || hasMetTarget) {
            return salary * 0.05; // 5% bonus
        } else {
            return 0.0; // No bonus
        }
    }
}


```

#### Casos de Teste - EmployeeBonus

1. **Bônus 15%:** Anos > 10 E metas=SIM → Salário 2000, 12 anos, metas=SIM → Resultado: 300
2. **Bônus 10%:** Anos > 5 E metas=SIM → Salário 2000, 7 anos, metas=SIM → Resultado: 200
3. **Bônus 5% (tempo):** Anos > 5 E metas=NÃO → Salário 2000, 8 anos, metas=NÃO → Resultado: 100
4. **Bônus 5% (meta):** Anos < 5 E metas=SIM → Salário 2000, 3 anos, metas=SIM → Resultado: 100
5. **Sem Bônus:** Anos < 5 E metas=NÃO → Salário 2000, 2 anos, metas=NÃO → Resultado: 0
6. **Fronteira - 5 Anos:** Anos = 5 E metas=NÃO → Salário 2000, 5 anos, metas=NÃO → Resultado: 0
7. **Fronteira - 10 Anos:** Anos = 10 E metas=SIM → Salário 2000, 10 anos, metas=SIM → Resultado: 200
