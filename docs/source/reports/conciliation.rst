##########################
Conciliações
##########################

Listar
======

::

    GET /api/v1/conciliations

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

* **machine_id**: o id da máquina das transações cashless.

  * Se passado, a consulta retorna somente transações cashless ocorridas nesta máquina.

* **kind**: o tipo das transações cashless.

  * Se passado, a consulta retorna somente transações cashless do tipo informado.

* **request_number**: o número da requisição das transações cashless.

  * Se passado, a consulta retorna somente transações cashless dessa requisição.

* **eft_provider_id**: o provedor de TEF das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse provedor TEF.

* **eft_authorizer_id**: o adquirente de TEF das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse adquirente.

* **eft_card_brand_id**: o cartão utilizado nas transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse cartão.

* **eft_card_type_id**: o tipo de cartão utilizado nas transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse tipo de cartão.

* **payment_authorizer_id**: o id do autorizador das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse autorizador.

* **masked_card_number**: o número do cartão mascarado das transações cashless.

  * Se passado, a consulta retorna somente transações cashless desse cartão.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem às transações cashless. O array é ordenado por data e hora das transações, da mais recente para a mais antiga. O campos de cada transação cashless são os seguintes:

* **occurred_at**: a data e hora da transação cashless, no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
* **kind**: o tipo da transação cashless
* **masked_card_number**: o número do cartão da transação cashless.
* **value**: o valor da transação cashless.
* **discount_value**: o valor do desconto da transação cashless.
* **request_number**: o número da requisição da transação cashless.
* **uuid**: o número do pedido caso exista.
* **eft_provider**: detalhes do provedor de TEF da transação cashless.
* **eft_authorizer**: detalhes do adquirente de TEF da transação cashless.
* **eft_card_brand**: detalhes do cartão utilizado na transação cashless.
* **eft_card_type**: detalhes do tipo de cartão utilizado na transação cashless.
* **payment_authorizer**: detalhes do autorizador do pagamento da transação cashless.

Segue um exemplo de retorno de consulta:

::

  [
    {
      "occurred_at": "2018-02-27T19:43:42.000Z",
      "kind": "eft_pinpad",
      "masked_card_number": "1111********0000",
      "value": 0.1,
      "discount_value": null,
      "request_number": "000237",
      "uuid": "f917b792-29e3-4378-b28f-d167fb19fbb0",
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
      "payment_authorizer": null
    },
    {
      "occurred_at": "2018-02-27T19:45:39.000Z",
      "kind": "eft_pinpad",
      "masked_card_number": null,
      "value": 0.1,
      "discount_value": null,
      "request_number": "000240",
      "uuid": null,
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
      "payment_authorizer": null
    }
  ]
