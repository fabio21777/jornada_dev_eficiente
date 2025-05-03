# Introdução ao Cognitive Driven Development (CDD)

Cognitive Driven Development (CDD) é uma abordagem de desenvolvimento que visa criar códigos e encontrar formas de limitar a quantidade de complexidade das unidades de código, definindo um limite de complexidade. Essa abordagem é fortemente inspirada na teoria da carga cognitiva.


Exemplo de metricas de complexidade com java

```java

/**
 * - classes de framework e libs não contam - 0 ICP
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
