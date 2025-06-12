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


## Validação de entrada

1. **limite o tamanho dos dados de entrada**: defina limites razoáveis para o tamanho dos dados de entrada, evitando ataques de negação de serviço (DoS) e consumo excessivo de recursos.
2. **vunerabilidade xml**: valide e saneie entradas XML para evitar injeções de entidades externas (XXE) e outras vulnerabilidades relacionadas a XML.
3. **valide os sqls**: sempre valide e saneie entradas SQL para evitar injeções SQL. Use consultas parametrizadas ou ORM para evitar injeções.
4. **valide os campos de entrada**: verifique se os campos de entrada atendem aos formatos esperados, como e-mails, números de telefone e valores numéricos.
5. **sempre limpe os dados de entrada**: remova caracteres indesejados, espaços em branco e outros elementos que possam causar problemas de segurança ou funcionalidade.
6. **overflow numero ou buffer**: proteja-se contra estouros de buffer e números, validando o tamanho e o tipo dos dados de entrada.
7. **entradas inválidas**: rejeite entradas que não atendam aos critérios de validação, como formatos incorretos, valores fora do intervalo esperado ou tipos de dados inválidos.
8. tratar exceções de forma adequada: implemente tratamento de exceções para lidar com erros de validação e fornecer feedback claro ao usuário sem expor detalhes técnicos.


## Log de erros e monitoramento

1. **Todas as Falhas de login devem ser registradas**: registre todas as tentativas de login, incluindo falhas, para monitorar atividades suspeitas.
2. **Segure os logs por tempo suficiente**: mantenha os logs por um período adequado para permitir a investigação de incidentes de segurança.
3. **Gere logs no formato legível**: use formatos de log legíveis e estruturados, como JSON ou CSV, para facilitar a análise e o monitoramento.
4. alertas de logs: implemente alertas para atividades suspeitas, como várias tentativas de login falhas, acessos não autorizados ou alterações inesperadas no sistema.
5. nunca log informações sensíveis: evite registrar informações confidenciais, como senhas, números de cartão de crédito ou dados pessoais, para proteger a privacidade dos usuários.

## Revisão de código com segurança em mente

1. **checklist de segurança**: crie uma checklist de segurança para revisar o código, incluindo práticas recomendadas e vulnerabilidades comuns.
2. **revisão de código por pares**: implemente revisões de código por pares para identificar problemas de segurança e garantir que as práticas recomendadas sejam seguidas.


## Use ferramentas de segurança de analise estática

1. leve a serio os feedbacks das ferramentas de segurança: use ferramentas de análise estática para identificar vulnerabilidades e problemas de segurança no código.

## Documentação de segurança

1. **documente as práticas de segurança**: mantenha uma documentação clara e atualizada sobre as práticas de segurança adotadas no projeto, incluindo políticas de acesso, criptografia e validação de entrada.
2. **Documente as melhores práticas de segurança**: crie um guia de melhores práticas de segurança para desenvolvedores, incluindo exemplos de código seguro e inseguro.

## Respondendo a atacantes

1. **Responda o mais rápido possível**: implemente um plano de resposta a incidentes para lidar com ataques e vulnerabilidades de forma rápida e eficaz.
2. **Delegue um security duty**: tenha um responsável pela segurança do projeto, que será o ponto de contato para questões de segurança e coordenará a resposta a incidentes.
3. **Trabalhe com a equipe**: colabore com a equipe de segurança para identificar e corrigir vulnerabilidades, garantindo que todos estejam cientes das práticas de segurança adotadas.
4. **Crie um framework de segurança**: desenvolva um framework de segurança que inclua diretrizes, ferramentas e processos para garantir a segurança do software desde o início do desenvolvimento.
5. **Cuidado com as informações sensíveis**: evite expor informações sensíveis, como chaves de API, senhas e dados pessoais, em repositórios públicos ou em código-fonte acessível.
6. **Organize as informações e o passo a passo seguido durante o ataque**: mantenha um registro detalhado das ações tomadas durante um incidente de segurança, incluindo a identificação da vulnerabilidade, as medidas corretivas e as lições aprendidas.
7. **Avalie o risco do ataque**: analise o impacto potencial do ataque e priorize as ações corretivas com base no risco associado.
8. **Impacto do ataque**: avalie o impacto do ataque na segurança, privacidade e integridade dos dados, bem como na reputação da organização.
9. **Classificação dos riscos**: classifique os riscos associados ao ataque, considerando a probabilidade de ocorrência e o impacto potencial.
10. **Postmortem**: após a resolução do incidente, realize uma análise pós-morte para identificar falhas no processo de segurança e implementar melhorias.
11. **Documente o processo de resposta a incidentes**: mantenha um registro detalhado das etapas tomadas durante a resposta ao incidente, incluindo a identificação da vulnerabilidade, as medidas corretivas e as lições aprendidas.
12. **Ações para que ataques similares não ocorram novamente**: implemente medidas corretivas para evitar que ataques semelhantes ocorram no futuro, como melhorias na segurança do código, treinamento da equipe e atualização de ferramentas de segurança.
