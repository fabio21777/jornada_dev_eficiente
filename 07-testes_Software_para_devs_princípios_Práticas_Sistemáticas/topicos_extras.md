# Tópicos Extras

## Flag de testes

> São testes intermitentes que às vezes falham, mesmo sem alteração no código.

Principais causas:

1. Concorrência
2. Uso incorreto de async/await
3. Dependências entre testes
4. Dependências externas

Como evitar testes flaky:

1. Escreva testes coesos e isolados
2. Evite dependências entre testes
3. Limpe os estados dos objetos e serviços que sofreram mudanças durante o teste

### O que fazer quando um teste flaky falhar?

1. Mover para uma suite de testes separada ("testes flaky")
2. Cemitério de testes: uma pasta onde os testes flaky são movidos para futuras correções
3. Executar o teste mais de uma vez para verificar se é realmente flaky
4. Deletar o teste, caso não seja possível corrigir ou isolar o problema

> Faça codigo simples, fácil de entender e fácil de manter. Testes devem ser simples e diretos, evitando complexidades desnecessárias que podem levar a testes flaky.


## Testes com microserviços

Priorize testes unitários e de integração, que a genade maioria dos tetse sejam unidades isoladas, sem dependências externas. Isso garante que os testes sejam rápidos, confiáveis e fáceis de manter. Mas devem ter testes end-to-end para validar a integração entre os microserviços e garantir que o sistema funcione como um todo.
