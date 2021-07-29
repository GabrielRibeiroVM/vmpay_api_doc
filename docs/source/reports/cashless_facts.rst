##########################
Transações cashless (Novo)
##########################

Listar
======

::

    GET /api/v1/cashless_facts

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **start_date**: a data de início das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas a partir desta data e hora, inclusive.
  * Deve-se passar a data e também a **hora**; se não passada, considerada-se 00:00 `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Um formato possível é *dd/mm/yyyy hh:mi:ss*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este campo também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
  * Caso o formato da data seja inválido, é retornado erro com o código HTTP 400 (*bad request*).

* **end_date**: a data final das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas até esta data e hora, inclusive.
  * Deve-se passar a data e também a **hora**; se não passada, considerada-se 00:00 `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Um formato possível é *dd/mm/yyyy hh:mi:ss*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este campo também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
  * Caso o formato da data seja inválido, é retornado erro com o código HTTP 400 (*bad request*).

* **client_id**: o id do cliente das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas para este cliente.

* **location_id**: o id do local das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas neste local.

* **place**: local interno da instalção.

  * Se passado, a consulta retorna somente transações cashless ocorridas neste local interno.

* **machine_type_id**: o id do tipo da máquina das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas neste tipo de máquina.

* **machine_id**: o id da máquina das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas nesta máquina.

* **distribution_center_id**: o id do centro de distribuição das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas nas instalações do centro de distribuição.

* **kind**: o tipo das transações cashless.

  * Se passado, a consulta retorna somente transações cashless do tipo informado.

* **point_of_sale**: o ponto de captura das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse ponto de captura.

* **request_number**: o número da requisição das transações cashless.

  * Se passado, a consulta retorna somente transações cashless dessa requisição.

* **route_id**: o id da rota associada a instalação das transações cashless.

  * Se passado, a consulta retorna somente transações cashless da instalação dessa rota.

* **eft_provider_id**: o provedor de TEF das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse provedor TEF.

* **eft_authorizer_id**: o adquirente de TEF das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse adquirente.

* **eft_card_brand_id**: o cartão utilizado nas transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse cartão.

* **eft_card_type_id**: o tipo de cartão utilizado nas transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse tipo de cartão.

* **good_category_id**: a categoria do produto das transações cashless.

  * Se passado, a consulta retorna somente transações cashless de produtos pertencentes a essa categoria.

* **good_manufacturer_id**: o fabricante do produto das transações cashless.

  * Se passado, a consulta retorna somente transações cashless de produtos pertencentes a esse fabricante.

* **good_id**: o produto das transações cashless.

  * Se passado, a consulta retorna somente transações cashless deste produto.
  * Tal produto pode ser composto (combo ou bebidas quentes) ou não (produtos vendidos por unidade).
  * `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.

* **customer_id**: o id do consumidor das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse consumidor.

* **status**: o status das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse status.
  * Valores possíveis:

  * *ok*: Transação OK.
  * *cancel*: Transação Cancelada.
  * *delivery_failure*: Falha na entrega.
  * *delivery_timeout*: Tempo de entrega esgotado.
  * *invalid_selection*: Seleção inválida.
  * *mdb_error*: Erro de MDB
  * *vending_invalid_no_second_selection*: Seleção inválida

* **equipment_id**: o id do equipamento das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse equipamento.

* **payment_authorizer_id**: o id do autorizador das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse autorizador.

* **masked_card_number**: o número do cartão mascarado das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse cartão.

* **product_type**: o tipo de produto das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse tipo de produto.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem às transações cashless. O array é ordenado por data e hora das transações, da mais recente para a mais antiga. O campos de cada transação cashless são os seguintes:

* **id**: o id da transação cashless.
* **occurred_at**: a data e hora da transação cashless, no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
* **point_of_sale**: o ponto de captura da transação cashless
* **kind**: o tipo da transação cashless
* **status**: o estado da transação cashless
* **installation_id**: o id da instalação da transação cashless.
* **planogram_item_id**: o id do item de planograma em que ocorreu a transação cashless (canaleta, seleção ou combo).
* **equipment_id**: o id do equipamento da transação cashless.
* **equipment_label_number**: o label do equipamento da transação cashless.
* **equipment_serial_number**: o número serial do equipamento da transação cashless.
* **masked_card_number**: o número do cartão da transação cashless.
* **number_of_payments**: o número de parcelas da transação cashless.
* **quantity**: a quantidade da transação cashless.
* **value**: o valor da transação cashless.
* **discount_value**: o valor do desconto da transação cashless.
* **request_number**: o número da requisição da transação cashless.
* **order_id**: o id do pedido da transação cashless.
* **cancel_reason_detailed**: a descrição do erro da transação cashless.
* **client**: detalhes do cliente da transação cashless.
* **location**: detalhes do local da transação cashless.
* **machine**: detalhes da máquina da transação cashless.
* **planogram_item**: o item de planograma em que ocorreu a transação cashless.
* **good**: detalhes do produto vendido na transação cashless.

  * * `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.

* **eft_provider**: detalhes do provedor de TEF da transação cashless.
* **eft_authorizer**: detalhes do adquirente de TEF da transação cashless.
* **eft_card_brand**: detalhes do cartão utilizado na transação cashless.
* **eft_card_type**: detalhes do tipo de cartão utilizado na transação cashless.
* **payment_authorizer**: detalhes do autorizador do pagamento da transação cashless.
* **mobile_app**: detalhes da aplicacao mobile onde ocorreu a transação cashless.
* **customer**: detalhes da consumidor da transação cashless.
* **cashless_error**: detalhes do erro caso tenha ocorrido na transação cashless.
* **cashless_error_friendly**: um booleano indicando se a transação foi ou não um crédito remoto.

Segue um exemplo de retorno de consulta:

::

    [
      {
        "id": 16732372,
        "occurred_at": "2018-02-28T21:34:21.000Z",
        "point_of_sale": "AA000009",
        "kind": "eft_pinpad",
        "status": "CANCEL",
        "installation_id": 9509,
        "planogram_item_id": null,
        "equipment_id": 1061,
        "equipment_label_number": "1064",
        "equipment_serial_number": "70B3D5CB818C",
        "masked_card_number": null,
        "number_of_payments": 0,
        "quantity": 1,
        "value": 0.1,
        "discount_value": null,
        "request_number": "",
        "order_id": null,
        "cancel_reason_detailed": "",
        "place": "Mesa do Fernandes",
        "client": {
          "id": 2854,
          "name": "Cliente virtual"
        },
        "location": {
          "id": 3515,
          "name": "Cliente virtual"
        },
        "machine": {
          "id": 3184,
          "asset_number": "1072"
        },
        "eft_provider": {
          "id": 2,
          "name": "SiTef"
        },
        "eft_authorizer": {
          "id": 5,
          "name": "Stone"
        },
        "eft_card_brand": {
          "id": 24,
          "name": "Indefinido"
        },
        "eft_card_type": {
          "id": 4,
          "name": "Indefinido"
        },
        "cashless_error": {
          "complete_description": "SiTef - -2 - Operação cancelada pelo operador."
        },
        "cashless_error_friendly": "Operação cancelada pelo operador."
      },
      {
        "id": 16660774,
        "occurred_at": "2018-02-27T19:53:16.000Z",
        "point_of_sale": "00020002101",
        "kind": "eft_pinpad",
        "status": "OK",
        "installation_id": 9509,
        "planogram_item_id": null,
        "equipment_id": 1061,
        "customer_id": null,
        "equipment_label_number": "1064",
        "equipment_serial_number": "70B3D5CB818C",
        "masked_card_number": null,
        "number_of_payments": 0,
        "quantity": 1,
        "value": 0.1,
        "discount_value": null,
        "request_number": "000246",
        "order_id": null,
        "cancel_reason_detailed": null,
        "place": "Mesa do Fernandes",
        "client": {
          "id": 2854,
          "name": "Cliente virtual"
        },
        "location": {
          "id": 3515,
          "name": "Cliente virtual"
        },
        "machine": {
          "id": 3184,
          "asset_number": "1072"
        },
        "eft_provider": {
          "id": 4,
          "name": "Indefinido"
        },
        "eft_authorizer": {
          "id": 7,
          "name": "Indefinido"
        },
        "eft_card_brand": {
          "id": 24,
          "name": "Indefinido"
        },
        "eft_card_type": {
          "id": 4,
          "name": "Indefinido"
        },
        "cashless_error_friendly": null
      }
    ]
