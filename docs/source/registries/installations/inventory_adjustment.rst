#####################
Ajustes de inventário
#####################

Listar
======

Lista os ajustes de invnetário de determinada máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/inventory_adjustments

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
===============  ================  ===========

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

* **start_date**: a data de início dos ajustes.

  * Se passado, a consulta retorna somente os ajustes ocorridos a partir desta data e hora, inclusive.
  * Deve-se passar a data e também a **hora**; se não passada, considerada-se 00:00 `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Um formato possível é *dd/mm/yyyy hh:mi:ss*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este campo também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
  * Caso o formato da data seja inválido, é retornado erro com o código HTTP 400 (*bad request*).

* **end_date**: a data final dos ajustes.

  * Se passado, a consulta retorna somente os ajustes ocorridos até esta data e hora, inclusive.
  * Deve-se passar a data e também a **hora**; se não passada, considerada-se 00:00 `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Um formato possível é *dd/mm/yyyy hh:mi:ss*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este campo também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
  * Caso o formato da data seja inválido, é retornado erro com o código HTTP 400 (*bad request*).

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  [
    {
      "id": 12314,
      "created_at": "2018-05-14T19:41:41.000Z",
      "planogram_id": 12332,
      "kind": "restock",
      "event_id": 33365598,
      "user_id": null,
      "occurred_at": "2017-11-06T13:15:37.000Z",
      "items": [
        {
          "id": 332154,
          "created_at": "2018-05-14T19:41:42.000Z",
          "added": 1,
          "removed": null,
          "observed": null,
          "balance_before": 0,
          "balance_after": 1,
          "final_balance_before": 2486,
          "final_balance_after": 2487,
          "planogram_item": {
            "id": 1613467,
            "created_at": "2017-08-28T18:41:20.000Z",
            "name": "PRODUTO 1",
            "capacity": 2600.0,
            "par_level": 2600.0,
            "good": {
              "id": 10324,
              "created_at": "2017-02-08T13:12:26.000Z",
              "name": "PRODUTO 1",
              "unit": {
                "id": 1,
                "fractionable": false,
                "name": "unit",
                "conversion_factor": 1
              }
            }
          }
        },
        {
          "id": 112457,
          "created_at": "2018-05-14T19:41:42.000Z",
          "added": 1,
          "removed": null,
          "observed": null,
          "balance_before": 0,
          "balance_after": 1,
          "final_balance_before": 2122,
          "final_balance_after": 2123,
          "planogram_item": {
            "id": 1613468,
            "created_at": "2017-08-28T18:41:20.000Z",
            "name": "PRODUTO 2",
            "capacity": 3500.0,
            "par_level": 3500.0,
            "good": {
              "id": 10322,
              "created_at": "2017-02-08T13:11:53.000Z",
              "name": "PRODUTO 2",
              "unit": {
                "id": 1,
                "fractionable": false,
                "name": "unit",
                "conversion_factor": 1
              }
            }
          }
        }
      ]
    },
    {
      "id": 104623,
      "created_at": "2017-10-31T17:13:31.000Z",
      "planogram_id": 12332,
      "kind": "now",
      "event_id": 381428824,
      "user_id": 472,
      "occurred_at": "2017-10-31T16:06:26.000Z",
      "items": [
        {
          "id": 859931,
          "created_at": "2017-10-31T17:13:31.000Z",
          "added": null,
          "removed": null,
          "observed": 200,
          "balance_before": 990,
          "balance_after": 200,
          "final_balance_before": 990,
          "final_balance_after": 200,
          "planogram_item": {
            "id": 1613471,
            "created_at": "2017-08-28T18:41:20.000Z",
            "name": "PRODUTO 3",
            "capacity": 1300.0,
            "par_level": 1300.0,
            "good": {
              "id": 10319,
              "created_at": "2017-02-08T12:31:44.000Z",
              "updated_at": "2017-02-13T16:23:30.000Z",
              "name": "PRODUTO 3",
              "unit": {
                "id": 1,
                "fractionable": false,
                "name": "unit",
                "conversion_factor": 1
              }
            }
          }
        }
      ]
    }
  ]

Ver
===

Mostra determinado ajuste de inventário de uma máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/inventory_adjustments/[id]

Parâmetros de URL:
------------------

===============  =======================  ===========
parâmetro        descrição                obrigatório
===============  =======================  ===========
machine_id       id da máquina            sim
installation_id  id da instalação         sim
id               id ajuste de inventário  sim
===============  =======================  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  {
    "id": 104623,
    "created_at": "2017-10-31T17:13:31.000Z",
    "planogram_id": 12332,
    "kind": "restock",
    "event_id": 381428824,
    "user_id": 472,
    "occurred_at": "2017-10-31T16:06:26.000Z",
    "items": [
      {
        "id": 859931,
        "created_at": "2017-10-31T17:13:31.000Z",
        "added": null,
        "removed": null,
        "observed": 200,
        "balance_before": 990,
        "balance_after": 200,
        "final_balance_before": 990,
        "final_balance_after": 200,
        "planogram_item": {
          "id": 1613471,
          "created_at": "2017-08-28T18:41:20.000Z",
          "name": "PRODUTO 3",
          "capacity": 1300.0,
          "par_level": 1300.0,
          "good": {
            "id": 10319,
            "created_at": "2017-02-08T12:31:44.000Z",
            "updated_at": "2017-02-13T16:23:30.000Z",
            "name": "PRODUTO 3",
            "unit": {
              "id": 1,
              "fractionable": false,
              "name": "unit",
              "conversion_factor": 1
            }
          }
        }
      }
    ]
  }

Campos
------

  * *id*: id do ajuste.
  * *created_at*: data de criação do ajuste.
  * *planogram_id*: id do planograma.
  * *kind*: tipo do ajuste.

    * Valores permitidos:

      * *initial* (quando ainda não existe nenhum reabastecimento)
      * *restock* (ajuste feito sobre o último reabastecimento)
      * *date* (baseado na data informada)
      * *now* (ajuste imediato)

  * *event_id*: id do evento.
  * *user_id*: id do usuário.
  * *occurred_at*: data de ocorrência do ajuste.
  * *items*: lista de itens do ajuste.

    * *id*: id do item
    * *created_at*: data de criação do item
    * *added*: quantidade adicionada
    * *removed*: quantidade removida
    * *observed*: quantidade observada
    * *balance_before*: balanço anterior
    * *balance_after*: balanço posterior
    * *final_balance_before*: balanço anterior final
    * *final_balance_after*: balanço posterior final
    * *planogram_item*: item do planograma

      * *id*: id do item de planograma
      * *created_at*: data de criação do item de planograma
      * *name*: descrição do item do planograma
      * *capacity*: capacidade
      * *par_level*: nível de par
      * *good*: produto associado ao item do planograma

        * *id*: id do produto
        * *created_at*: data de criação do produto
        * *updated_at*: data de alteração do produto
        * *name*: descrição do produto
        * *unit*: unidade do produto

Erros
-----

======  ======================================================  =========================================
status  descrição                                               response body
======  ======================================================  =========================================
404     máquina/instalação/ajuste de inventário não encontrado  { "status": "404", "error": "Not Found" }
======  ======================================================  =========================================

Criar
=====

Cria um ajuste de inventário.

::

  POST /api/v1/machines/[machine_id]/installations/[installation_id]/inventory_adjustments

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
===============  ================  ===========

Request::

  {
    "inventory_adjustment": {
      "planogram_id": 12332,
      "kind": "restock",
      "occurred_at": "2017-11-06 11:15:37 -0200",
      "items_attributes": [{
        "planogram_item_id": 1613467,
        "balance_before": 0,
        "added": "1",
        "removed": "",
        "observed": ""
      }, {
        "planogram_item_id": 1613468,
        "balance_before": 0,
        "added": "1",
        "removed": "",
        "observed": ""
      }]
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *inventory_adjustment*

  * *planogram_id*: id do planograma.
  * *kind*: tipo do ajuste.

    * Valores permitidos:

      * *initial* (ajuste efetuado em uma nova instalação, sem reabastecimento prévio efetuado)
      * *restock* (ajuste feito sobre o último reabastecimento)
      * *now* (ajuste imediato)

  * *occurred_at*: data de ocorrência do ajuste.
  * *items_attributes*: lista com os dados dos itens de planograma

    * *planogram_item_id*: id do item de planograma.
    * *balance_before*: balanço anterior.
    * *added*: quantidade adicionada.
    * *removed*: quantidade removida.
    * *observed*: quantidade observada.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 104623,
    "created_at": "2017-10-31T17:13:31.000Z",
    "planogram_id": 12332,
    "kind": "restock",
    "event_id": 381428824,
    "user_id": 472,
    "occurred_at": "2017-10-31T16:06:26.000Z",
    "items": [
      {
        "id": 859931,
        "created_at": "2017-10-31T17:13:31.000Z",
        "added": null,
        "removed": null,
        "observed": 200,
        "balance_before": 990,
        "balance_after": 200,
        "final_balance_before": 990,
        "final_balance_after": 200,
        "planogram_item": {
          "id": 1613471,
          "created_at": "2017-08-28T18:41:20.000Z",
          "name": "PRODUTO 3",
          "capacity": 1300.0,
          "par_level": 1300.0,
          "good": {
            "id": 10319,
            "created_at": "2017-02-08T12:31:44.000Z",
            "updated_at": "2017-02-13T16:23:30.000Z",
            "name": "PRODUTO 3",
            "unit": {
              "id": 1,
              "fractionable": false,
              "name": "unit",
              "conversion_factor": 1
            }
          }
        }
      }
    ]
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
404         máquina/instalação não encontrada     { "status": "404", "error": "Not Found" }
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar::

  {
    "items.balance_after": [
      "deve ser maior ou igual a 0"
    ],
    "items.final_balance_after": [
      "deve ser maior ou igual a 0"
    ],
    "base": [
      "Instalação não possui reabastecimento para ser ajustado"
    ]
  }
