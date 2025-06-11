# Arquitetura de sistemas enterprise


## Escalabilidade

1. Replicação de dados(apenas leitura), delação de dados, sharding, particionamento de dados.
2. Cache(redis, em memoria) - complexidade adicional, no mecanimso de cache, invalidação de cache, consistência eventual.
3. Escalabilidade horizontal - adicionar mais máquinas, balanceamento de carga, replicação de dados como escalonamneto horizontal regional.
4. Sistemas reativos - responsivos, resilientes, elásticos e orientados a mensagens.


## tradoff

1. consistencia eventual
2. processamento assíncrono
3. Banco de dados distribuído
4. chache


> ETL: Extract, Transform, Load
> ETL é um processo de extração, transformação e carregamento de dados. É usado para integrar dados de diferentes fontes em um único repositório, como um data warehouse. O processo envolve a extração de dados de fontes diversas, a transformação desses dados para garantir consistência e qualidade, e o carregamento dos dados transformados em um sistema de destino.
