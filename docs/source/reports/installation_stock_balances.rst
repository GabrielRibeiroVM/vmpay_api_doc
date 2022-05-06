##########################
Saldos das instalações
##########################

Listar
======

::

    GET /api/v1/installation_stock_balances

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **client_id**: o id do cliente das instalações.

  * Se passado, a consulta retorna somente saldos da instalações do cliente.

* **location_id**: o id do local das instalações.

  * Se passado, a consulta retorna somente instalações deste local.

* **machine_id**: o id da máquina das instalações.

  * Se passado, a consulta retorna somente instalações desta máquina.

* **machine_type_id**: o id do tipo de máquina das instalações.

  * Se passado, a consulta retorna somente instalações desse tipo de máquina.

* **machine_model_id**: o id modelo de máquina das instalações.

  * Se passado, a consulta retorna somente instalações desse modelo de máquina.

* **category_id**: o id da categoria dos produtos das instalações.

  * Se passado, a consulta retorna somente instalações de produtos desta categoria.

* **good_id**: o id do produto das instalações.

  * Se passado, a consulta retorna somente instalações deste produto.
  * Tal produto pode ser composto (combo ou bebidas quentes) ou não (produtos vendidos por unidade).
  * `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.

* **product_type_id**: o id do tipo de produto das instalações.

  * Se passado, a consulta retorna somente instalações desse tipo de produto.

* **use_cost_price**: utiliza preço de custo (true/false).

  * Se passado true, o sistema considera o campo preço de custo informado no produto.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem às transações cashless. O array é ordenado por data e hora das transações, da mais recente para a mais antiga. O campos de cada transação cashless são os seguintes:

* **client**: detalhes do cliente da transação cashless.
* **location**: detalhes do local da transação cashless.
* **machine**: detalhes da máquina da transação cashless.
* **good**: detalhes do produto vendido.
* **inventory_balance**: o valor da transação cashless.
* **desired_price**: o valor do desconto da transação cashless.

Segue um exemplo de retorno de consulta:

::

  [
    {
      "client": {
        "id": 2703,
        "name": "Cliente 1"
      },
      "location": {
        "id": 4590,
        "name": "Local 1"
      },
      "machine": {
        "id": 1809,
        "asset_number": "0010"
      },
      "good": {
        "id": 6424,
        "upc_code": "1",
        "barcode": 123456789,
        "name": "Água Mineral"
      },
      "inventory_balance": 18,
      "desired_price": 36.0
    },
    {
      "client": {
        "id": 2702,
        "name": "Cliente 2"
      },
      "location": {
        "id": 4591,
        "name": "Local 2"
      },
      "machine": {
        "id": 1810,
        "asset_number": "0011"
      },
      "good": {
        "id": 11,
        "upc_code": "88",
        "barcode": 111111111,
        "name": "Castanha de Caju"
      },
      "inventory_balance": 10,
      "desired_price": 60.0
    }
  ]
