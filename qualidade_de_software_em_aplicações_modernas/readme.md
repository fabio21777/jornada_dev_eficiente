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

## Domine sua IDE


