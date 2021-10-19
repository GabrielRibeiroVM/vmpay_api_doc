####################
Perguntas frequentes
####################

O VMpay pode ser integrado com outros sistemas?
===============================================

Sim, o sistema VMpay disponibiliza várias APIs que possibilitam a integração com todos os sistemas do mercado.

A integração é realizada através de APIs padrão REST que enviam e recebem dados no formato JSON.

Com essas APIs é possível consultar, incluir, alterar, excluir e listar os dados do sistema VMpay.

Basta consultar o manual da API e utilizar o seu token de acesso para iniciar a integração.


Como obtenho meu token de acesso?
=================================

Basta solicitar a seu token de acesso junto ao operador. Esta chave é obtida no sistema VMpay pelo menu *Configurações > Chaves de operador*.

De posse desta chave, o desenvolvedor deverá passar o parâmetro **access_token** em todas as URLs, conforme o exemplo abaixo:

::

  https://vmpay.vertitecnologia.com.br/api/v1/caminho/para/api?access_token=837e068fbb4c1e1f


Há um ambiente de homologação para APIs?
========================================

Sim, o VMpay possui um ambiente de homologação.

Para obter um token para acesso ao ambiente de homologação solicite diretamente à equipe de suporte.

**Importante ¹:** O token de acesso à API de homologação é diferente do token da API de produção.

**Importante ²:** A VM não realiza sincronização entre a base de homologação e a base de produção, sendo que o operador será responsável por popular e manter ambas as bases.


Como utilizar a paginação?
==========================

Abaixo alguns exemplos do relatório de invoices, passando o parâmetro de datas de 01/01/2021 até 30/01/2021.

Exemplo 1
---------

Sem usar os parâmetros **page** e **per_page**: Neste exemplo, irá retornar apenas a página 1 com no máximo 100 registros.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021

Exemplo 2
---------

Usando apenas o parâmetro **per_page**: Neste exemplo o retorno será de 1000 registros e apenas a pagina 1.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021&per_page=1000

Exemplo 3
---------

Usando os parâmetros **page** e **per_page**: Neste exemplo o retorno será de 1000 registros e a página 3 de acordo com os parâmetros passados.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021&per_page=1000&page=3


Como sei qual é a última página?
================================

Em seu código você deverá incrementar o parâmetro page até que o número de registros retornados seja menor que o número passado no parâmetro per_page.


Como consulto o estoque nas minhas máquinas via API?
====================================================

Todos os ajustes de inventário e reabastecimentos são realizados nas instalações e atualizam os saldos dos produtos no último planograma cadastrado.

Para consultar o estoque atual de cada instalação utilize a `API de planograma <registries/installations/planogram.html>`_.


Como consulto o estoque do centro de distribuição via API?
==========================================================

**Importante:** Caso deseje utilizar essa funcionalidade, solicite ao suporte que habilite a função de controle de estoque para seu operador.

O cliente pode possuir um ou mais centros de distribuição para reabastecimento de suas máquinas/instalações no sistema.

Para consultar o estoque dos centros de distribuição utilize a `API de estoque <inventory/storable.html>`_.
