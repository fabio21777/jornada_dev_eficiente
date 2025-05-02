# Qualidade de Software em Aplicações Modernas

Antes de qualquer técnica, conceitos, design ou fundamentos, a primeira preocupação deveria ser escrever um código que possa ser lido e mantido por outros programadores.

## Ser fluido na aplicação dos conceitos

A partir dos conceitos, aplique os conhecimentos em projetos reais, com o objetivo de criar aplicações que sejam fáceis de entender e manter.

## Conheça as tecnologias

Por exemplo, a criação de uma *constraint* para validar se um valor é único em um banco de dados, utilizando o Hibernate Validator e o Spring Framework. Um detalhe importante é que o padrão *bean* exige a existência de um construtor padrão, ou seja, um construtor sem parâmetros. Porém, no contexto do Spring, o construtor padrão é opcional, pois o Spring pode injetar dependências diretamente nos campos da classe. Isso significa que você pode usar a injeção de dependência diretamente nos campos sem precisar de um construtor padrão. Entender o framework que está utilizando é essencial para compreender como ele funciona e como pode ser utilizado para resolver problemas específicos.

```java
public class UniqueValueValidator implements ConstraintValidator<UniqueValue, Object> {

    private String domainAttribute;
    private Class<?> klass;
    private EntityManager manager;

    public UniqueValueValidator(EntityManager manager) {
        this.manager = manager;
    }

    @Override
    public void initialize(UniqueValue params) {
        domainAttribute = params.fieldName();
        klass = params.domainClass();
    }

    @Override
    public boolean isValid(Object value, ConstraintValidatorContext context) {
        Query query = manager.createQuery("select 1 from " + klass.getName() + " where " + domainAttribute + " = :value");
        query.setParameter("value", value);
        List<?> list = query.getResultList();

        Assert.state(list.size() <= 1, "Foi encontrado mais de um " + domainAttribute + " com o valor " + value);

        return list.isEmpty();
    }
}
```

## História no formato para o programador

Escrever uma história no formato para o programador é importante para tangibilizar o que deve ser feito. Esse documento, que é rápido de criar, pode ser usado para esclarecer as ideias sobre o desenvolvimento e também como um double-check para verificar se o que foi escrito é realmente o que deve ser implementado.

### Exemplo de um endpoint de um sistema de cadastro de usuários:

1. Criar um endpoint para cadastrar um usuário.
2. O endpoint deve ser acessível apenas para usuários autenticados.
3. O endpoint deve receber os seguintes parâmetros:
   - Nome
   - Email
   - Senha (A senha deve ser criptografada).
4. O endpoint deve validar se o email já está cadastrado.
5. Utilizar o Hibernate Validator para validar e persistir o usuário.
6. O endpoint deve retornar o usuário cadastrado.
7. O endpoint deve retornar um erro caso o email já esteja cadastrado.
8. O endpoint deve retornar um erro caso o usuário não esteja autenticado.

## Design de código

São decisões e definições que tomamos no dia a dia na escrita do código. São as pequenas decisões no momento da codificação, com o objetivo de criar um código que seja fácil de entender e manter. O design de código é uma parte importante do desenvolvimento de software, pois ajuda a garantir que o código seja legível, reutilizável e fácil de modificar.


## CDD

[Minhas notas cdd](./cdd.md)




## Modificação pode ser mais fácil que extensão

é um principio do solid o 'O', que diz o seguinte:
> "Um módulo deve ser fechado para modificação, mas aberto para extensão". Isso significa que devemos evitar modificar o código existente, mas podemos estender o código existente para adicionar novas funcionalidades. Isso ajuda a garantir que o código existente permaneça estável e não seja afetado por mudanças futuras.
>

Normalmente as modificações são mais fácieis do que extensões, criar abtroçoes generalistas demais podem aumentar a a complexidade do código sem adicionar fluidez na codigificação, apesar de ser um principio importante, o O do SOLID, com oqualquer outro princípio, deve ser aplicado conforme a necessidade e contexto do prolema.

## Acoplamento com o framework

Os frameworks mais modernos, como Spring Boot, Quarkus e Micronaut, normalmente geram pouco acoplamento, e o nível de código geralmente ocorre apenas via metadados (anotações), o que facilita a migração. Aqui pode ser levado em consideração um tradeoff importante: o quanto de facilidade de codificação e manutenção será obtido ao se acoplar ao framework, e o quanto de acoplamento será gerado. O ideal é que o acoplamento seja o menor possível, mas isso pode gerar um aumento na complexidade do código, dificultando a manutenção e a codificação.

## DTOs com métodos

DTOs (Data Transfer Objects) são objetos que transportam dados entre processos. Eles são usados para transferir dados entre a camada de apresentação e a camada de serviço, ou entre a camada de serviço e a camada de persistência. Os DTOs ajudam a evitar o acoplamento entre as camadas e garantem que os dados sejam transferidos de forma eficiente.

Uma reflexão válida é a adição de métodos nos DTOs. Em alguns casos, isso pode fazer sentido, como, por exemplo, passar o `EntityManager` como parâmetro para buscar uma entidade específica, em vez de criar um novo serviço apenas para essa função. No entanto, essa abordagem deve ser usada dependendo do contexto e da complexidade do sistema.


## Preciso de um monte de camadas (arquiteturas em camadas)?

A arquitetura em camadas é uma abordagem comum no desenvolvimento de software, onde o sistema é dividido em camadas distintas, cada uma com sua própria responsabilidade. O core da aplicação fica "protegido e desacoplado" de outras partes do sistema.

Apesar de ser uma abordagem com suas vantagens, normalmente o custo para manter e codificar é maior, e o tempo de desenvolvimento também aumenta. Embora seja uma estratégia válida, é importante sempre avaliar o contexto e verificar se os trade-offs são adequados para o problema em questão.

## Acoplamento mental

O acoplamento mental ocorre devido a decisões de código normalmente influenciadas por bibliotecas ou frameworks que seguem determinados padrões. Um exemplo disso foi uma busca específica no Elasticsearch, onde a consulta era construída concatenando strings separadas por espaços e, posteriormente, realizando um split nesses espaços para obter os atributos corretamente.

Esse tipo de acoplamento mental exige que a pessoa que está mantendo ou evoluindo o código leia e compreenda detalhadamente o que está acontecendo. Isso pode ser um problema se a pessoa não estiver familiarizada com a biblioteca ou framework utilizado, levando a erros e dificuldades na manutenção do código.

Para evitar esse tipo de acoplamento, é importante adotar práticas que tornem o código mais claro e menos dependente de detalhes específicos de implementação.

## Abrace o lagado

O legado é uma parte importante do desenvolvimento de software, e muitas vezes é necessário lidar com sistemas legados que não foram projetados com as melhores práticas em mente. Em vez de tentar reescrever todo o sistema legado, o ideal é entender como ele funciona e como pode ser melhorado.

## Bateria de testes automatizados

1. Aumenta a confiabilidade do código.
2. Aumenta a quantidade de código a ser mantido.
3. Melhora a confiança da equipe, pois valida futuras correções, evoluções e refatorações na base de código.



