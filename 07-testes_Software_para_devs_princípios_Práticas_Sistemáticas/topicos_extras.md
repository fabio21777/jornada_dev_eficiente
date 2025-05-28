# Tópicos Extras

## Flag de testes

> São testes intermitentes que às vezes falham, mesmo sem alteração no código.

Principais causas:

1. Concorrência
2. Uso incorreto de async/await
3. Dependências entre testes
4. Dependências externas

Como evitar testes flaky:

1. Escreva testes coesos e isolados.
2. Evite dependências entre testes.
3. Limpe os estados dos objetos e serviços que sofreram mudanças durante o teste.

### O que fazer quando um teste flaky falhar?

1. Mova para uma suíte de testes separada ("testes flaky").
2. Cemitério de testes: uma pasta onde os testes flaky são movidos para futuras correções.
3. Execute o teste mais de uma vez para verificar se é realmente flaky.
4. Delete o teste, caso não seja possível corrigir ou isolar o problema.

> Faça código simples, fácil de entender e fácil de manter. Testes devem ser simples e diretos, evitando complexidades desnecessárias que podem levar a testes flaky.

---

## Testes com microserviços

Priorize testes unitários e de integração, garantindo que a grande maioria dos testes sejam de unidades isoladas, sem dependências externas. Isso garante que os testes sejam rápidos, confiáveis e fáceis de manter. No entanto, também é importante ter testes end-to-end para validar a integração entre os microserviços e garantir que o sistema funcione como um todo.

## Como testar sistema legado

> Sistema difícil de testar

Refatore sempre que possível, porém na indústria quase sempre é inviável refatorar todo o sistema.

1. Entenda por que é difícil testar o sistema.
2. Crie infraestrutura (libs/APIs de testes) que permita testar partes do sistema de forma isolada.

### Como criar essa infraestrutura

1. Como colocar o sistema em um estado conhecido.
2. Como executar o caso de uso de maneira fácil.
3. Como observar o comportamento do sistema.
