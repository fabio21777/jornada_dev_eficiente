# Desenvolvimento Seguro de Software

## Controle de Acesso identidade e autenticação

1. **Siga o princípio do menor privilégio**, garantindo que os usuários tenham apenas as permissões necessárias para realizar suas tarefas.
2. **Os usuario não podem obter mais acesso apenas ajustanto a solicitação de acesso**, evitando que usuários comuns possam solicitar permissões administrativas.
3. Usuarios comuns não devem ter acesso a recursos administrativos, como a api de alteração de permissões.
4. restrição para metodos que alteram o estado do sistema, como POST, PUT, DELETE, PATCH.
5. **Imponha limites de taxa (rate limiting)** para evitar abusos e ataques de força bruta.
6. **limite e atrase as tentativas de login** para prevenir ataques de força bruta.
7. **Monitoramento e auditoria**: implemente logs de acesso e ações dos usuários para detectar atividades suspeitas.

## Falhas criptograficas

1. **sempre criptografe dados sensíveis**, como senhas, números de cartão de crédito e informações pessoais.
2. **evite armazenar dados sensíveis, o faça apenas quando necessário** e sempre criptografados.
3. **quais algoritmos criptográficos usar?** Use algoritmos modernos e seguros, como AES para criptografia simétrica e RSA ou ECC para criptografia assimétrica.
4. **Nunca use seus próprios algoritmos criptográficos**, a menos que você seja um especialista em criptografia.
5. **Use funções de geração de aleatoridade reconhecidas e seguras**, como aquelas fornecidas por bibliotecas padrão ou APIs de criptografia.
6. **Use sempre HTTPS para comunicação segura** entre o cliente e o servidor, evitando a exposição de dados sensíveis em texto claro.
7. **permita apenas viveeis criptgraficos corretos e seguros**, como TLS 1.2 ou superior.

## Injeção de dados

1. **sql injection**: sempre use consultas parametrizadas ou ORM para evitar injeções SQL.
2. **injeção de comandos**: nunca confie em entradas do usuário para construir comandos do sistema operacional. Use APIs seguras para executar comandos.
3. **injeção de ognl**: evite usar OGNL ou outras linguagens de expressão que permitam a execução de código arbitrário. Use bibliotecas seguras para manipulação de dados.
4. **injeção de XML e json**: valide e saneie entradas XML para evitar injeções de entidades externas (XXE) e outras vulnerabilidades relacionadas a XML.
5. **Nunca confie em entradas do usuário**: sempre valide e saneie entradas do usuário antes de processá-las, independentemente do tipo de injeção.


## Configurações incorretas

1. **evite configurações padrão inseguras**: altere senhas padrão, desative serviços desnecessários e configure corretamente os sistemas.
2. **evite paginas desnecessárias**: remova páginas de administração, documentação e outras páginas que não são necessárias para o funcionamento do sistema.
3. **evite mensagens de erros como stack traces**: não exponha detalhes técnicos em mensagens de erro, pois isso pode ajudar atacantes a explorar vulnerabilidades.
4. **use sempre variáveis de ambiente para configurações sensíveis**: como senhas, chaves de API e outras informações confidenciais, evitando armazená-las no código-fonte.


