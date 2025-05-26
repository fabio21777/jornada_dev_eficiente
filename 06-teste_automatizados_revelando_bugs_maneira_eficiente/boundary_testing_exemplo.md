# Boundary Testing com JUnit - Exemplo Completo

## Classe Testada

```java
public class IdadeValidator {

    public boolean podeEntrar(int idade) {
        return idade >= 18;
    }

    public String validarIdade(int idade) {
        if (idade < 0) {
            return "Idade inválida";
        } else if (idade < 18) {
            return "Menor de idade";
        } else {
            return "Maior de idade";
        }
    }
}
```

## Teste com JUnit Parameterized

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import org.junit.jupiter.params.provider.ValueSource;
import static org.junit.jupiter.api.Assertions.*;

class IdadeValidatorTest {

    private IdadeValidator validator = new IdadeValidator();

    @ParameterizedTest(name = "Idade {0}: {1}")
    @CsvSource({
        "-1, false,  'Valor inválido - idade negativa (fronteira inferior extrema)'",
        "0,  false,  'Valor mínimo possível - recém nascido'",
        "17, false,  'Último valor inválido - um dia antes da maioridade'",
        "18, true,   'Fronteira crítica - exatamente na idade mínima permitida'",
        "19, true,   'Primeiro valor após fronteira - confirmação de aceitação'",
        "65, true,   'Valor alto mas válido - pessoa idosa'",
        "120, true,  'Valor extremo alto - limite teórico de idade humana'"
    })
    void testePodeEntrar(int idade, boolean esperado, String comentario) {
        // Executa o teste
        boolean resultado = validator.podeEntrar(idade);

        // Verifica o resultado com mensagem personalizada
        assertEquals(esperado, resultado,
            String.format("Falha para idade %d: %s", idade, comentario));
    }

    @ParameterizedTest(name = "Validação completa - Idade {0}")
    @CsvSource({
        "-5,  'Idade inválida',  'Fronteira negativa - valor impossível'",
        "0,   'Menor de idade',  'Recém nascido - início da vida'",
        "17,  'Menor de idade',  'Véspera da maioridade - ainda menor'",
        "18,  'Maior de idade',  'Marco legal - transição para adulto'",
        "19,  'Maior de idade',  'Confirmação pós-fronteira - adulto jovem'",
        "30,  'Maior de idade',  'Adulto consolidado - meio da faixa válida'",
        "100, 'Maior de idade',  'Centenário - extremo superior realista'"
    })
    void testeValidacaoCompleta(int idade, String esperado, String comentario) {
        String resultado = validator.validarIdade(idade);

        assertEquals(esperado, resultado,
            String.format("Falha na validação da idade %d: %s", idade, comentario));
    }

    // Teste adicional focado apenas na fronteira crítica
    @ParameterizedTest(name = "Fronteira crítica: {0}")
    @ValueSource(ints = {16, 17, 18, 19, 20})
    void testeFronteiraCritica(int idade) {
        boolean podeEntrar = validator.podeEntrar(idade);
        String validacao = validator.validarIdade(idade);

        if (idade < 18) {
            assertFalse(podeEntrar, "Menor de 18 não deveria poder entrar");
            assertEquals("Menor de idade", validacao);
        } else {
            assertTrue(podeEntrar, "Maior ou igual a 18 deveria poder entrar");
            assertEquals("Maior de idade", validacao);
        }
    }
}
```

## Análise dos Valores de Teste

### Partições Identificadas:

- **Inválidas**: idades < 0 (impossíveis)
- **Menores**: 0 ≤ idade < 18 (válidas mas insuficientes)
- **Maiores**: idade ≥ 18 (válidas e suficientes)

### Fronteiras Testadas:

1. **Fronteira Inferior Extrema**: -1, 0 (valores impossíveis/mínimos)
2. **Fronteira Crítica**: 17, 18, 19 (transição menor/maior)
3. **Fronteira Superior**: 65, 100, 120 (valores altos mas possíveis)

### Comentários dos Casos:

- **-1**: Testa validação de entrada inválida
- **0**: Valor mínimo tecnicamente possível
- **17**: Último valor que falha no critério
- **18**: **Valor crítico** - exatamente no limite legal
- **19**: Confirma que a fronteira está correta
- **65+**: Testa comportamento em idades avançadas

## Execução

```bash
# Para executar os testes
mvn test

# Saída esperada mostrará cada caso com seu comentário:
# ✓ Idade -1: Valor inválido - idade negativa (fronteira inferior extrema)
# ✓ Idade 18: Fronteira crítica - exatamente na idade mínima permitida
# etc.
```

## Vantagens desta Abordagem

1. **Cobertura Máxima**: Testa todos os pontos críticos com poucos casos
2. **Documentação**: Comentários explicam o propósito de cada teste
3. **Manutenibilidade**: Fácil adicionar novos casos na anotação `@CsvSource`
4. **Clareza**: Nomes descritivos mostram exatamente o que está sendo testado

Esta estratégia de boundary testing garante que os erros mais comuns (off-by-one, operadores incorretos) sejam detectados eficientemente.
