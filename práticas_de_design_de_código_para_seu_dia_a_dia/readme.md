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
	public void exexuta(@PathVariable Long idConta,@RequestHeader("id-pessoa-logada") , @RequestBody NovoConviteRequest request) {
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
