# Introdução ao Cognitive Driven Development (CDD)

Cognitive Driven Development (CDD) é uma abordagem de desenvolvimento que visa criar códigos e encontrar formas de limitar a quantidade de complexidade das unidades de código, definindo um limite de complexidade. Essa abordagem é fortemente inspirada na teoria da carga cognitiva.
Para construir um código de qualidade, é necessário entender a complexidade do código e como ela pode afetar a manutenção e a evolução do software. O CDD é uma abordagem que busca reduzir essa complexidade, tornando o código mais legível e fácil de entender no longo prazo.
O CDD não é sobre não usar Clean Architecture, Clean Code, SOLID, padrões de projeto, etc. O CDD é sobre como usar essas técnicas e padrões de forma a reduzir ou não aumentar a complexidade do código. O CDD é uma abordagem que busca reduzir a complexidade do código, tornando-o mais legível e fácil de entender no longo prazo.
A premissa base do CDD é fazer código que caiba na mente de uma pessoa. Como referência, o artigo "Magical Number Seven, Plus or Minus Two" de George A. Miller, que sugere que a capacidade de processamento cognitivo humano é limitada a cerca de sete elementos (mais ou menos dois) em um único momento. Isso significa que, ao projetar sistemas e interfaces, devemos considerar essa limitação e tentar manter a complexidade dentro desse limite.

## Teoria da carga cognitiva

A teoria da carga cognitiva é um conceito da psicologia educacional que se refere à quantidade de esforço mental que uma pessoa precisa empregar para aprender ou realizar uma tarefa. Essa teoria sugere que a capacidade de processamento cognitivo humano é limitada, e que essa limitação pode afetar a aprendizagem e o desempenho em tarefas complexas.

- **Medida**: A medida é uma regra fixa, geralmente apoiada em um padrão ou convenção.
- **Avaliação**: A avaliação é uma regra subjetiva, que depende do contexto e do conhecimento prévio do avaliador.

### Intrinsic Complex Point (ICP)

O ICP é um ponto de complexidade. São as unidades de complexidade que podem ser medidas e utilizadas para calcular a complexidade de uma unidade de código. O ICP é uma métrica que mede a complexidade intrínseca de um ponto de código, levando em consideração fatores como o número de variáveis, o número de condições e o número de loops. Idealmente, o ICP deve ser calculado em um nível de granularidade que faça sentido para o contexto do código. É uma métrica importante para medir a qualidade do código.

No caso do Java, recomenda-se que seja feito para a classe inteira, ou seja, o ICP deve ser calculado para a classe inteira. Isso significa que todas as variáveis, condições e loops da classe devem ser considerados ao calcular o ICP. O ICP deve ser calculado em um nível de granularidade que faça sentido para o contexto do código.



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
