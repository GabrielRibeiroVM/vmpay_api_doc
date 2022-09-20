#############
Notas Fiscais
#############

Listar
======

::

    GET /api/v1/invoices

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **start_date**: a data de início das notas fiscais.

  * A consulta retorna somente notas fiscais geradas a partir desta data e hora, inclusive.
  * Este filtro é **obrigatório**. Se não for passado, será retornado erro com o código HTTP 400 (*bad request*).
  * Se o formato da data for inválido, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for maior que a do filtro *end_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for menor que 30 dias antes da data do filtro *end_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Deve-se passar a data e também a **hora**; se não for passada, será considerado **00:00:00** `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Os segundos passados na hora são desconsiderados. O sistema considera sempre **00**.
  * Um formato possível é *dd/mm/yyyy hh:mi*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este filtro também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.

* **end_date**: a data final das notas fiscais.

  * A consulta retorna somente notas fiscais geradas até esta data e hora, inclusive.
  * Este filtro é **obrigatório**. Se não for passado, será retornado erro com o código HTTP 400 (*bad request*).
  * Se o formato da data for inválido, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for menor que a do filtro *start_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for maior que 30 dias depois da data do filtro *start_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Deve-se passar a data e também a **hora**; se não for passada, será considerado **23:59:59** `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Os segundos passados na hora são desconsiderados. O sistema considera sempre **59**.
  * Um formato possível é *dd/mm/yyyy hh:mi*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este filtro também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.

* **client_id**: o id do cliente das notas fiscais. Se passado, a consulta retorna somente notas fiscais geradas por esse cliente.

* **location_id**: o id do local das notas fiscais. Se passado, a consulta retorna somente notas fiscais geradas neste local.

* **machine_id**: o id da máquina das notas fiscais. Se passado, a consulta retorna somente notas fiscais geradas nesta máquina.

* **customer_email**: o e-mail do consumidor informado na compra. Se passado, a consulta retorna somente notas fiscais geradas com esse e-mail.

* **status**: indica qual o status que deseja consultar, podendo ser um desses valores:

  * *pending*: Nota fiscal pendente de envio.
  * *issuing*: Nota fiscal sendo enviada.
  * *issued*: Nota fiscal emitida.
  * *failed*: Falha na emissão da nota fiscal.
  * *error*: Erro na emissão da nota fiscal.
  * *cannot_issue*: Nota fiscal não emitida.
  * *issued_in_staging*: Nota fiscal emitida em ambiente de homologação.

* **number**: número da nota fiscal. Se passado, a consulta retorna somente a nota fiscal com esse número.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem às visitas. O array é ordenado por data e hora de geração da nota fiscal, da mais recente para a mais antiga. O campos de cada nota fiscal são os seguintes:

* **id**: o id da nota fiscal.
* **occurred_at**: a data e hora da nota fiscal, no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
* **uuid**: o uuid da nota fiscal.
* **series**: a serie da nota fiscal.
* **number**: o número da nota fiscal.
* **customer_document**: o documento do consumidor.
* **customer_email**: o e-mail do consumidor.
* **status**: o status atual da nota fiscal.
* **total_quantity**: a quantidade total dos itens da nota fiscal.
* **total_amount**: o valor total dos itens da nota fiscal.
* **installation_id**: o id da instalação da nota fiscal.
* **customer**: id e nome do consumidor.
* **client**: id e nome do cliente.
* **location**: o id e nome do local.
* **machine**: o id e número de fábrica da máquina.
* **danfe_url**: a url para baixar o danfe da nota fiscal.
    * Caso a emissão da Nota Fiscal seja via SAT, para acessar a URL deve ser informado o "access_token": https://vmpay.vertitecnologia.com.br/api/v1/invoices/4/sat_data_pdf?access_token=837e068fbb4c1e1f
* **xml_url**: a url para baixar o xml da nota fiscal.
    * Caso a emissão da Nota Fiscal seja via SAT, para acessar a URL deve ser informado o "access_token": https://vmpay.vertitecnologia.com.br/api/v1/invoices/4/sat_data?access_token=837e068fbb4c1e1f
* **routes**: array com detalhes das rotas da instalação da nota fiscal.
* **items**: array com os itens da nota fiscal.
* **payment**: informações sobre a forma de pagamento, se disponível.

Segue um exemplo de retorno de consulta:

::

  [
    {
      "id": 4,
      "occurred_at": "2021-03-16T15:12:51.000Z",
      "uuid": "fba266ce-1d05-4a0b-be63-87bf965c0c17",
      "series": "15",
      "number": "289692",
      "customer_document": "32376582865",
      "customer_email": null,
      "status": "issued",
      "total_quantity": 1,
      "total_amount": 16.99,
      "installation_id": 1,
      "customer": {
        "id": 1,
        "name": "Consumidor"
      },
      "client": {
        "id": 2703,
        "name": "Verti"
      },
      "location": {
        "id": 1,
        "name": "Verti"
      },
      "machine": {
        "id": 1,
        "asset_number": "0001"
      },
      "danfe_url": "https://api.focusnfe.com.br/notas_fiscais_consumidor/NFe1111.html",
      "xml_url": "https://api.focusnfe.com.br/arquivos/21590391000111/202103/XMLs/1111-nfe.xml",
      "routes": [],
      "items": [
        {
          "number": 1,
          "price": 16.99,
          "quantity": 1.0,
          "amount": 16.99,
          "good": {
            "id": 5,
            "name": "Budweiserr",
            "upc_code": "1"
          }
        }
      ],
      "payment": {
        "request_number": "1",
        "eft_provider_id": 2,
        "eft_authorizer_id": 3,
        "eft_card_brand_id": 4,
        "eft_card_type_id": 5,
        "number_of_payments": 1,
        "kind": "external_authorizer_vmlink",
        "payment_authorizer": {
          "id": 2,
          "name": "PicPay"
        }
      }
    },
    {
      "id": 3,
      "occurred_at": "2021-03-16T10:01:56.000Z",
      "uuid": "0765b0c7-584d-47da-bd21-ff79f8e33bc0",
      "series": null,
      "number": "085662",
      "customer_document": null,
      "customer_email": null,
      "status": "issued",
      "total_quantity": 2,
      "total_amount": 11.48,
      "installation_id": 1,
      "customer": {
        "id": 2,
        "name": "Consumidor"
      },
      "client": {
        "id": 2703,
        "name": "Verti"
      },
      "location": {
        "id": 1,
        "name": "Verti"
      },
      "machine": {
        "id": 1,
        "asset_number": "0001"
      },
      "danfe_url": "https://api.focusnfe.com.br/notas_fiscais_consumidor/NFe2222.html",
      "xml_url": "https://api.focusnfe.com.br/notas_fiscais_consumidor/NFe2222.html",
      "routes": [],
      "items": [
        {
          "number": 1,
          "price": 6.49,
          "quantity": 1.0,
          "amount": 6.49,
          "good": {
            "id": 2,
            "name": "Coca-Cola",
            "upc_code": "2"
          }
        },
        {
          "number": 2,
          "price": 4.99,
          "quantity": 1.0,
          "amount": 4.99,
          "good": {
            "id": 12,
            "name": "Twix",
            "upc_code": "3"
          }
        }
      ]
    }
  ]
