####################
Perguntas frequentes
####################

O VMpay pode ser integrado com outros sistemas?
===============================================

Sim, o sistema VMpay disponibiliza várias APIs que possibilitam a integração com todos os sistemas do mercado.

A integração é realizada através de APIs padrão REST que enviam e recebem dados no formato JSON.

Com essas APIs é possível consultar, incluir, alterar, excluir e listar dos dados do sistema VMpay.

Basta consultar o manual da API e utilizar o seu token de acesso para iniciar a integração.


Como obtenho meu token de acesso?
==================================

Basta solicitar a seu token de acesso junto ao operador. Esta chave é obtida no sistema VMpay pelo menu Configurações > Chaves de operador.

De posse desta chave, o desenvolvedor deverá passar o parâmetro **access_token** em todas as URLs, conforme o exemplo abaixo:

::

  https://vmpay.vertitecnologia.com.br/api/v1/caminho/para/api?access_token=837e068fbb4c1e1f


Tem uma base teste para APIs?
=============================

Sim, o VMpay possui uma base teste.

Para obter um token para acesso à API de teste solicite diretamente à equipe de suporte.

**Importante ¹:** O token de acesso à API de teste é diferente do token da API de produção.

**Importante ²:** a VM não realiza sincronização entre a base de testes e a base de produção, sendo que o operador será responsável por popular e manter ambas as bases.


Como utilizar a paginação?
==========================

Abaixo alguns exemplos do relatório de invoices, passando o parâmetro de datas de 01/01/2021 até 30/01/2021.

Exemplo 1
---------

Sem parâmetros page e per_page, neste exemplo, irá retornar apenas uma página com no máximo 100 registros.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021

Exemplo 2
---------

Com apenas parâmetro per_page, neste exemplo o retorno trara 1000 registros e apenas a pagina 1.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021&per_page=1000

Exemplo 3
---------

Com parâmetro per_page e page, neste exemplo o retorno trará todos os dados de acordo com o filtro passado.

::

  https://vmpay.vertitecnologia.com.br/api/v1/invoices?access_token=837e068fbb4c1e1f&start_date=01/01/2021&end_date=30/01/2021&per_page=1000&page=3


Como sei qual é a última página?
===========================================================

Em seu código você deverá incrementar o parâmetro page até que o número de registros retornados seja menor que o número passado no parâmetro per_page.


Como consulto o estoque nas minhas máquinas via API?
====================================================

A consulta de estoque nas máquinas é acessado via API do planograma que mostra o estoque atual de produtos por máquina. Todos os ajustes de inventário e reabastecimento são realizados nas instalações e atualizam o saldo do produto no ultimo planograma cadastrado.

Para consultar o estoque de cada instalação utilize a `API de planograma <registries/installations/planogram.html>`_.


Como consulto o estoque dos meus centros de distribuição via API?
=================================================================

O cliente pode possuir um ou mais centro de distribuição para reabastecimento de suas máquinas/instalações, neste caso são criados os centros de distribuição no sistema e vinculado a uma ou mais máquinas de acordo com a operação do cliente.

Para consultar o estoque dos centros de distribuição utilize a `API de estoque <inventory/storable.html>`_.

**Atenção:** Caso deseje utilizar essa funcionalidade, solicite ao suporte que habilite a função de controle de estoque para seu operador.
