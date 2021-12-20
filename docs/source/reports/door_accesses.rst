##################
Abertura de Portas
##################

Listar
======

::

    GET /api/v1/door_accesses

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **client_id**: o id do cliente da abetura da porta.

  * Se passado, a consulta retorna somente abertura de portas ocorridos neste cliente.

* **location_id**: o id do local da abetura da porta.

  * Se passado, a consulta retorna somente abertura de portas ocorridos neste local.

* **machine_id**: o id da máquina da abetura da porta.

  * Se passado, a consulta retorna somente abertura de portas ocorridos nesta máquina.

* **email**: o email do market_user da abertura de porta.

  * Se passado, a consulta retorna somente abertura de portas desse usuário.

* **name**: o nome do market_user da abertura de porta.

  * Se passado, a consulta retorna somente abertura de portas desse usuário.

* **cpf**: o cpf do market_user da abertura de porta.

  * Se passado, a consulta retorna somente abertura de portas desse usuário.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem aos alertas. O array é ordenado por data e hora de alerta, da mais recente para a mais antiga. O campos de cada alerta são os seguintes:

* **occurred_at**: a data e hora do alerta, no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
* **client**: detalhes do cliente da abertura de porta.
* **location**: detalhes do local da abertura de porta.
* **machine**: detalhes da máquina da abertura de porta.
* **equipment**: equipamento da abertura de porta.
* **market_user**: detalhes do usuário da abertura de porta.

Segue um exemplo de retorno de consulta:

::

  [
    {
      "occurred_at": "2020-06-01T17:44:23.000Z",
      "client": {
         "id": 112,
         "name": "Verti Tecnologia"
      },
      "location": {
         "id": 197,
         "name": "Sede Verti"
      },
      "machine": {
         "id": 1,
         "asset_number": "0001"
      },
      "equipment": " ( - VMbox)",
      "market_user": {
        "id": 2,
        "name": "Usuário 1",
        "email": "email@vertitecnologia.com.br",
        "cpf": "14567800077",
        "born_on": "1979-01-01"
      }
    },
    {
      "occurred_at": "2020-06-02T17:44:23.000Z",
      "client": {
         "id": 112,
         "name": "Verti Tecnologia"
      },
      "location": {
         "id": 197,
         "name": "Sede Verti"
      },
      "machine": {
         "id": 1,
         "asset_number": "0001"
      },
      "equipment": " ( - VMbox)",
      "market_user": {
        "id": 3,
        "name": "Usuário 2",
        "email": "email2@vertitecnologia.com.br",
        "cpf": "19967803412",
        "born_on": "1985-01-01"
      }
    }
]
