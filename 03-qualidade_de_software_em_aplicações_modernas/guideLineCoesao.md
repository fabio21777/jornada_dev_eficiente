# [voltar](guideline.md)


## Guia para coesão
A coesão é uma métrica que mede o quanto os métodos de uma classe estão relacionados entre si. Uma classe deve ter um único propósito, e todos os métodos devem estar relacionados a esse propósito. Isso facilita a manutenção e a evolução do código, pois mudanças em um método não afetam outros métodos que não estão relacionados.


## Maximize a coesão do código
Constantemente analise se o código que você está escrevendo tem conexão com os outros códigos já escritos. Tente manter tudo que faz sentido ficar junto, realmente próximo. Alguns exemplos da aplicação dessa ideia:

1. Se você tem uma classe que tem um atributo de data e você precisa saber se determinado objeto tem um valor antes ou depois daquela data, você deveria criar um método dentro daquela classe para operar sobre o atributo.
2. Se você decidiu criar um novo serviço, maximize a chance de que todo código daquele serviço realmente tenha conexão.
