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


> Lei de conway
>1. **Organizações que projetam sistemas são limitadas a projetar sistemas que >refletem suas estruturas de comunicação**.


## Papéis e responsabilidades


