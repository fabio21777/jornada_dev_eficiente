# Arquitetura de sistemas enterprise

## Escalabilidade

1. Replicação de dados (apenas leitura), deleção de dados, sharding, particionamento de dados.
2. Cache (Redis, em memória) – adiciona complexidade, principalmente nos mecanismos de cache, invalidação e consistência eventual.
3. Escalabilidade horizontal – adicionar mais máquinas, balanceamento de carga, replicação de dados como escalonamento horizontal regional.
4. Sistemas reativos – responsivos, resilientes, elásticos e orientados a mensagens.

### Trade-offs

1. Consistência eventual
2. Processamento assíncrono
3. Banco de dados distribuído
4. Cache

> **ETL: Extract, Transform, Load**
> ETL é um processo de extração, transformação e carregamento de dados. É usado para integrar dados de diferentes fontes em um único repositório, como um data warehouse. O processo envolve a extração de dados de fontes diversas, a transformação desses dados para garantir consistência e qualidade, e o carregamento dos dados transformados em um sistema de destino.

## Autonomia

## Arquitura baseado em eventos

  - fazer com que os sitemas se comuniquem por meio de eventos, para comunicação
  - dificil de coodenarr
  - acoplamento
  - debugar difícil
  - comunicação entre equipes
  - sitemas de tentativa e erro

## Eventos separam os consumidores dos produtores

desvantagens:
1. Dificuldade de depuração
2. dificl de monitorar


## Microserviços

1. frontreira entre os serviços pode ser uma tarefa complexa
2. Soluçõo para times e não solução tecnológica
3. Times pequenos e autônomos
4. sistemas distribuídos é difícil tecnicamente falando

## Topologias de times (team topologies - matthew skelton e manuel pais)

## Four team types

1. Stream-aligned team - focada em um fluxo de trabalho específico, como uma funcionalidade ou produto.
2. Enabling team - ajuda outras equipes a superar obstáculos e melhorar suas habilidades.
3. Complicated Subsystem team - lida com partes complexas do sistema que exigem especialização técnica.
4. Platform team - fornece uma plataforma comum para outras equipes, facilitando o desenvolvimento e a integração.


## Three Interaction Modes

> **Lei de Conway:**
> Organizações que projetam sistemas são limitadas a projetar sistemas que refletem suas estruturas de comunicação.

## Papéis e responsabilidades

(Descreva aqui os principais papéis e responsabilidades dos times e profissionais envolvidos na arquitetura de sistemas enterprise.)

## Infraestrutura e plataformas

### Cloud native e self-service

1. **Cloud native:** Aplicações projetadas para serem executadas na nuvem, aproveitando recursos de escalabilidade, resiliência e flexibilidade.
2. **Dimensionamento horizontal:** Capacidade de adicionar mais instâncias para lidar com aumento de carga.
3. **Independência de local:** Aplicações que podem ser executadas em qualquer ambiente de nuvem.
4. **Efêmera:** Instâncias podem ser criadas e destruídas rapidamente, sem dependência de estado local.
5. **Replicável:** Facilidade para replicar ambientes e aplicações.
6. **Uso das APIs da nuvem:** Integração nativa com os serviços oferecidos pela nuvem.
7. **Multi-nuvem:** Capacidade de operar em diferentes provedores de nuvem (cloud agnostic), utilizando ferramentas e APIs de cada nuvem.
8. **Times de plataforma:** Times que criam e mantêm plataformas de desenvolvimento, oferecendo serviços e ferramentas para outras equipes.

## Qualidade

1. **Reúso de código:**
   - Normalmente é muito difícil reutilizar código entre sistemas diferentes, especialmente em sistemas distribuídos.
   - Pode haver repetição de bugs.
   - Compartilhar demais significa muito acoplamento.

2. **Dívida técnica:**
   - Todos os sistemas têm dívida técnica, que é o custo de manter e evoluir o código existente.
   - Pode atrasar o desenvolvimento no longo prazo.
   - Modularização ruim.
   - Testes ruins.
   - Falta de documentação.
   - Falta de propriedade do código.
   - Uso de tecnologia desatualizada ou interna.

3. **Evite refatoração big bang:**
   - Refatoração big bang é uma abordagem onde todo o código é reescrito de uma só vez, o que pode ser arriscado e difícil de gerenciar.
   - É melhor fazer refatorações incrementais, melhorando pequenas partes do código ao longo do tempo.

4. **Lute contra a dívida técnica:**
   - É importante combater a dívida técnica, priorizando melhorias contínuas no código e na arquitetura.
   - Isso envolve refatoração constante, testes automatizados e documentação adequada.

5. **Testes:**
   - **Fast tests:** Testes rápidos que verificam a funcionalidade básica do sistema.
   - **Integration tests:** Testes que verificam a integração entre diferentes componentes do sistema.
   - **Manual tests:** Testes manuais realizados por desenvolvedores ou testadores para verificar a funcionalidade do sistema.
