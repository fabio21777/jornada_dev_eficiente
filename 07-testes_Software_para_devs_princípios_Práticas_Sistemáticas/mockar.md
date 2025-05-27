# Por que mockar, eis a questão

Mockar é uma técnica que permite simular o comportamento de objetos ou componentes externos, facilitando a criação de testes unitários.

### Quando usar mocks

Utilize mocks para componentes que dificultam a criação de testes, como por exemplo:

- Acesso a banco de dados
- Chamadas a APIs externas
- Interações com sistemas externos

### Quando não usar mocks

Evite mocks quando o objetivo do teste é validar a funcionalidade principal do caso de uso, como por exemplo:

- Verificar se uma query retorna as informações corretas
- Garantir que um objeto está sendo persistido corretamente no banco de dados
- Validar se o endpoint está retornando o status correto

Também não é recomendado mockar entidades que representam o domínio do sistema, como por exemplo:

- DTOs
- Entidades
- Classes de domínio em geral
- Métodos utilitários que não dependem de sistemas externos

### Internal ou peer: uma ótima maneira de classificar dependências

1. **Internal**: Dependências internas são aquelas que pertencem à mesma funcionalidade, sendo componentes separados apenas para facilitar a manutenção e evolução do código. Por serem parte fundamental do que deve ser testado, essas dependências não devem ser mockadas.
2. **Peer**: Dependências peer são aquelas que pertencem a funcionalidades diferentes, mas que interagem entre si. Essas dependências normalmente podem ser mockadas. Um exemplo comum são os repositórios.

### Fakes, stubs e mocks

1. **Stubs** – Objetos que retornam valores pré-definidos, sem lógica de negócio. São usados para simular o comportamento de dependências externas.
2. **Fakes** – Objetos que implementam uma lógica de negócio simples, mas não são tão complexos quanto os objetos reais. São usados para simular o comportamento de dependências externas de forma mais realista (por exemplo, um banco de dados em memória como H2).
3. **Mocks** – Objetos que verificam se métodos específicos foram chamados com os parâmetros corretos. São usados para validar interações entre componentes e é possível fazer asserções sobre o comportamento do código.

### Quais os problemas de mockar demais?


1. **Acomplamento entre classes**: Mockar demais pode levar os teste a acomplarem demais com a implementação, tornando-os frágeis e difíceis de manter.
2. **Contrato do moc e do componente precisam evoluir juntos**: Os testes devem ser modificados sempre que o contrato do mock ou do componente mudar, o que pode aumentar a complexidade e o custo de manutenção dos testes.
