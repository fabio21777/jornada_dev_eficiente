# Design para Testes

## Arquitetura Hexagonal (Ports and Adapters)

A arquitetura hexagonal, também conhecida como "Ports and Adapters", é um padrão de arquitetura que tem como objetivo isolar a lógica de negócio dos detalhes de infraestrutura, como bancos de dados, frameworks, APIs externas, etc.

### Princípios

- **Separação de responsabilidades:** Não misture lógica de negócio com detalhes de infraestrutura.
- **Priorize a lógica de interface e de negócio:** A lógica central da aplicação deve ser independente de detalhes externos.
- **Evite que a "sujeira" da infraestrutura contamine a lógica de negócio:** Adapte a infraestrutura à lógica de negócio, e não o contrário.

> Ao adotar a arquitetura hexagonal, você garante que sua lógica de negócio pode ser testada de forma isolada, sem dependências externas, tornando os testes mais rápidos, confiáveis e fáceis de escrever.



