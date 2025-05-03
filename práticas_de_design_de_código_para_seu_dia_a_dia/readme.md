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

