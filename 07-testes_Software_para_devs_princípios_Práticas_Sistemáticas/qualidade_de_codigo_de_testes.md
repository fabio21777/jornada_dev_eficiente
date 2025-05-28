# Qualidade de Código de Testes

## Características de um bom teste

1. **Coeso, independente e isolado:**
   Cada teste deve ser responsável por uma única funcionalidade ou comportamento do código, sem depender de outros testes ou do ambiente.

2. **Relevante:**
   O teste deve ter uma boa razão para existir, sendo necessário e relevante para o código que está sendo testado.

3. **Repetitivo, determinístico e não flaky:**
   Os testes devem produzir sempre os mesmos resultados, independentemente do ambiente ou da ordem de execução. Testes instáveis ("flaky") podem gerar falsos positivos ou negativos, dificultando a confiança nos resultados.

4. **Quebra com mudança de código:**
   Se um teste falhar após uma alteração no código, isso indica que a mudança afetou o comportamento esperado, ajudando a identificar regressões.

5. **Falha com motivo claro:**
   Quando um teste falha, deve ser fácil identificar a causa do problema, facilitando a depuração e a correção do código.

6. **Fácil de ler:**
   O código do teste deve ser claro e fácil de entender, facilitando a manutenção e a correção em caso de falhas.

7. **Fácil de modificar e evoluir:**
   O teste deve ser projetado para ser facilmente atualizado conforme o código evolui, garantindo que permaneça relevante e eficaz ao longo do tempo.

## Testes sem asserção

Testes sem asserção devem ser evitados, pois não validam o comportamento esperado do código.
