# [volta](../readme.md)

# Prática

Praticar é descrever, explicarar e aplicar o conhecimento adquirido. A prática é fundamental para a retenção do conhecimento e para a aplicação em situações reais. A pratica é para atigir o objetivo definido do objetivo.

## Plano de aprendizagem

[Plano de aprendizagem](Plano_Aprendizagem.md)

## Prática prioritaria

A prática prioritária é a prática que deve ser feita primeiro, pois é a prática que mais se aproxima do objetivo definido. A prática prioritária deve ser feita com o máximo de atenção e dedicação, pois é a prática que mais irá contribuir para o aprendizado.

* Progressão da dificuldade
* Variação de dificuldade e contexto

## Prática de suporte

São as práticas como anotações, resumos, mapas mentais, flashcards, etc. Essas práticas são importantes para a retenção do conhecimento e para a aplicação em situações reais. A prática de suporte deve ser feita com o máximo de atenção e dedicação, pois é a prática que mais irá contribuir para o aprendizado.

1. **Anotações**: As anotações são uma forma de registrar o conhecimento adquirido. Elas podem ser feitas em papel ou digitalmente, e devem ser feitas com o máximo de atenção e dedicação, pois são as anotações que mais irão contribuir para o aprendizado.
2. **Resumos**: Os resumos são uma forma de condensar o conhecimento adquirido. Eles podem ser feitos em papel ou digitalmente, e devem ser feitos com o máximo de atenção e dedicação, pois são os resumos que mais irão contribuir para o aprendizado.
3. **Analise de código**: A análise de código é uma forma de entender o funcionamento de um determinado código. Ela pode ser feita em papel ou digitalmente, e deve ser feita com o máximo de atenção e dedicação, pois é a análise de código que mais irá contribuir para o aprendizado.


## Prática acessória

É prática de prática de uma parte do conhecimento adquirido. Elas podem ser feitas em grupo ou individualmente, e devem ser feitas com o máximo de atenção e dedicação, pois são as práticas acessórias que mais irão contribuir para o aprendizado, por exemplo, o estudo de como funcionar o hibernate, que apenas a parte de persistência do spring mvc, ou estudar o junit5, que apenas a parte de testes do java, ou estudar o spring security, que apenas a parte de segurança do spring mvc.

### Exemplo de prática de suporte

* Criar um post n estilo de blog
* criar um quiz com chat gpt
* Resumo para outras pessoas no formato de explicação


## Atividades de recuperação

As atividades de recuperação são atividades que ajudam a fixar o conhecimento adquirido. Essas atividades podem ser feitas em grupo ou individualmente, e devem ser feitas com o máximo de atenção e dedicação, pois são as atividades que mais irão contribuir para o aprendizado.

## A importância da prática deliberada


### 10 Exercícios de Desenvolvimento de APIs com Spring Boot(Exemplo)

| Exercício | O quão fácil eu sinto que vai ser implementar? | Detalhamento passo a passo do que vou implementar | O quão fácil foi? | Analisando o que eu fiz (Debriefing, retrospectiva) | Minha solução passou no critério de aceite | Nível de dificuldade |
|-----------|------------------------------------------------|--------------------------------------------------|-------------------|-----------------------------------------------------|-------------------------------------------|---------------------|
| **1. Cadastro de Produtos** <br>*Sem Relacionamentos* | Sistema simples sem relacionamentos, será fácil de implementar com CRUD básico | 1. Criar entidade Produto (nome, preço, descrição, estoque)<br>2. Criar repository, service e controller<br>3. Implementar operações CRUD<br>4. Adicionar funcionalidades de atualização de estoque e descontos | | | | 1 - Muito fácil |
| **2. Cadastro de Tarefas** <br>*Sem Relacionamentos* | API básica com filtragem simples, não deverá apresentar grandes dificuldades | 1. Criar entidade Tarefa (título, descrição, status, data vencimento)<br>2. Implementar CRUD básico<br>3. Adicionar filtros por status<br>4. Implementar marcação de conclusão | | | | 2 - Fácil |
| **3. Cliente e Endereço** <br>*Relacionamento 1:1* | Relacionamento 1:1 exigirá atenção na configuração das entidades e persistência | 1. Modelar entidades Cliente e Endereço<br>2. Configurar relacionamento @OneToOne<br>3. Implementar CascadeType para persistência conjunta<br>4. Criar endpoints para gerenciamento | | | | 3 - Médio |
| **4. Veículo e Registro** <br>*Relacionamento 1:1* | Similar ao exercício anterior, mas com validações adicionais | 1. Criar entidades Veículo e RegistroPropriedade<br>2. Configurar relacionamento bidirecional<br>3. Implementar validações específicas<br>4. Garantir integridade do relacionamento | | | | 3 - Médio |
| **5. Pedidos e Clientes** <br>*Relacionamento 1:N* | Exigirá atenção na modelagem do relacionamento e nas consultas | 1. Modelar entidades Cliente e Pedido<br>2. Configurar @OneToMany e @ManyToOne<br>3. Implementar endpoints para listar pedidos por cliente<br>4. Criar validações para integridade referencial | | | | 4 - Difícil |
| **6. Cursos e Departamentos** <br>*Relacionamento 1:N* | Estrutura similar ao exercício anterior, mas com lógica de negócio diferente | 1. Modelar entidades Departamento e Curso<br>2. Configurar relacionamentos<br>3. Implementar listagem de cursos por departamento<br>4. Criar métodos para gerenciamento dos relacionamentos | | | | 4 - Difícil |
| **7. Cursos e Alunos** <br>*Relacionamento N:M* | Relacionamento mais complexo, exigirá tabela intermediária | 1. Modelar entidades Curso e Aluno<br>2. Configurar @ManyToMany<br>3. Criar classe de relacionamento Matrícula se necessário<br>4. Implementar endpoints para matrícula e consultas | | | | 4 - Difícil |
| **8. Livros e Autores** <br>*Relacionamento N:M* | Relacionamento N:M com regras de negócio específicas | 1. Modelar entidades Livro e Autor<br>2. Configurar relacionamento @ManyToMany<br>3. Implementar operações de associação<br>4. Criar endpoints para consultas bidirecionais | | | | 4 - Difícil |
| **9. E-commerce** <br>*Múltiplos Relacionamentos* | Sistema complexo com diversos tipos de relacionamentos | 1. Modelar entidades (Produto, Categoria, Pedido, Cliente, Carrinho)<br>2. Configurar relacionamentos diversos<br>3. Implementar regras de negócio para carrinho e pedidos<br>4. Criar endpoints para operações comuns de e-commerce | | | | 5 - Muito difícil |
| **10. Sistema Universitário** <br>*Desafio Avançado* | Sistema altamente complexo com múltiplos relacionamentos e recursos avançados | 1. Modelar entidades principais do domínio acadêmico<br>2. Implementar todos os tipos de relacionamentos<br>3. Adicionar autenticação JWT e controle de acesso<br>4. Integrar com APIs externas<br>5. Criar dashboard analítico | | | | 5 - Muito difícil |

## Tecnologias Recomendadas

- Spring Boot
- Spring Data JPA
- Spring Security
- Hibernate
- MySQL/PostgreSQL/H2
- Maven/Gradle

## Critérios de Aceite Gerais

1. API deve seguir os princípios REST
2. Todas as operações CRUD devem funcionar corretamente
3. Relacionamentos entre entidades devem ser corretamente configurados
4. Tratamento adequado de exceções
5. Testes unitários e integração devem passar



## Repetição espaçada

A repetição espaçada é uma técnica de aprendizado que envolve revisar o material em intervalos crescentes de tempo. Essa técnica é baseada na ideia de que a memória humana tende a esquecer informações ao longo do tempo, e revisitar o material em momentos estratégicos pode ajudar a reforçar o aprendizado e melhorar a retenção a longo prazo(Como anki).


