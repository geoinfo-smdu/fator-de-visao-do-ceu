# Fator de Visão do Céu

Repositório de desenvolvimento e testes metodológicos para determinar o fator de visão do céu no município de São Paulo

## Motivação

A Cidade de São Paulo possui um levantamento LiDAR 3D de toda a sua área. Muitas análises podem ser feitas a partir desse sensoriamento.
Pretendemos portanto utilizar esse repositório para desenvolver e testar métodos de análise do levantamento da superfície 3D da cidade.
Começaremos por análises relativas aos Sistemas de Espaçõs Livres, e especificamente sobre a quantificação e o mapeamento do Fator de Visão do Céu (Sky View Factor)

## Metodologia

Separamos 3 áreas urbanas distintas da cidade, cujo os arquivos estão disponibilizados aqui, e a partir dessas áreas amostrais, vamos desenvolver e testar as análises propostas.
As áreas correspondem aos seguintes SCMs (Sistema Cartográfico Metropolitano):

* Centro: 3314-231
* Vila Andrade: 3331-132
* São Mateus: 4331-222

A primeira proposta de análise é criar uma abstração de uma semi esfera sobre cada ponto do solo e a partir desse ponto visualizar porções de mesma área dessa semi esfera. A partir da contagem das áreas da semi esfera que fazem contato direto com esse ponto teremos possibilidade de quantificar a área visível de céu.

Portanto temos uma primeira questão que seria dividir essa semi esfera em partes com a mesma área de forma homogênea. Como referência para isso temos [este artigo de Matt Hancock](http://notmatthancock.github.io/2017/12/26/regular-area-sphere-partitioning.html) 

Inicialmente podemos pensar em dividir a esfera em 256 partes, que é um número de base 4, além de ocupar apenas 1 byte de tamanho e parece que suficiente para calculos da escala urbana que daria incrementos de cerca de 0,39%.

Dentre diversas estratégias teríamos duas situações para pensar o algorítimo:

* Gerar um raster a partir do MDS com cerca de 1 metro de resolução; e calcular um HillShade para cada uma das 256 faces da semi esfera, calculando seu azimuth e altura.
* A partir de cada ponto no ground MDT, criar 256 sólidos, sendo um para cada área da semi esfera, e contar quantos desses sólidos intersectam algum ponto.

## Gerando um raster a partir do MDS

Para testar uma das possibilidades, vamos criar um raster com um metro de resolução a partir do MDS LiDAR. Para isso vamos usar a biblioteca PDAL, utilizando o seguinte comando:

`pdal pipeline arquivos/MDS_1metro.json`

## Contribuições

As contribuições são muito bem vindas, estimulam a cidadania e contribuem para a compreensão da cidade e podem ensejar uma discussão técnica sobre o planejamento urbano.
