########
Máquinas
########

Listar
======

::

  GET /api/v1/machines

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Datas devem ser
passadas no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.

* **asset_number**: filtra máquinas pelo número de patrimônio.
* **tags**: filtra máquinas pelas tags passadas em um array.

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo:

::

  [
    {
      "id": 42,
      "machine_model_id": 82,
      "asset_number": "M010 - 0037",
      "external_id": null,
      "distribution_center_id": 47,
      "tags": ["tag1", "tag2"],
      "installation": {
        "id": 1106,
        "location_id": 1391,
        "machine_id": 42,
        "equipment_id": 999,
        "place": "the bad place",
        "cash_mode": "cash_and_cashless",
        "restock_mode": "restock_and_cash_collect",
        "notifications_enabled": false
      }
    },
    {
      "id": 222,
      "machine_model_id": 75,
      "asset_number": "M003 - 0009",
      "external_id": null,
      "distribution_center_id": 47,
      "tags": ["tag1", "tag3"]
    }
  ]

Ver
===

::

  GET /api/v1/machines/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da máquina    sim
=========  ===============  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo:

::

  {
    "id": 42,
    "machine_model_id": 82,
    "asset_number": "M010 - 0037",
    "external_id": null,
    "distribution_center_id": 47,
    "tags": ["tag1", "tag2"],
    "installation": {
      "id": 1106,
      "location_id": 1391,
      "machine_id": 42,
      "equipment_id": 999,
      "place": "the bad place",
      "cash_mode": "cash_and_cashless",
      "restock_mode": "restock_and_cash_collect",
      "notifications_enabled": false
    }
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         máquina não encontrada    { "status": "404", "error": "Not Found" }
==========  ========================  =========================================

Criar
=====

::

  POST /api/v1/machines

Request::

  {
    "machine": {
      "asset_number": "01234",
      "machine_model_id": "12",
      "external_id": "qwe123",
      "tags": ["tag1", "tag2"]
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *machine*

  * *asset number*: número de patrimônio.
  * *machine_model_id*: id do modelo da máquina.

Opcionais
^^^^^^^^^

* *machine*

  * *external_id*: identificador externo da máquina.
  * *tags*: array com tags.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 614,
    "machine_model_id": 12,
    "asset_number": "01234",
    "external_id": "qwe123",
    "tags": ["tag1", "tag2"]
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "machine_model_id": [
      "não pode ficar em branco"
    ],
    "asset_number": [
      "já está em uso"
    ]
  }

Atualizar
=========

::

  PATCH /api/v1/machines/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da máquina    sim
=========  ===============  ===========

Request::

  {
    "machine": {
      "asset_number": "998877",
      "tags": ["tag1", "tag2"]
    }
  }

Campos
------

Ao menos um campo interno a *machine* deve ser passado.

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo::

  {
    "id": 612,
    "machine_model_id": 69,
    "asset_number": "998877",
    "external_id": null,
    "distribution_center_id": 47,
    "tags": ["tag1", "tag2"],
    "installation": {
      "id": 1119,
      "location_id": 185,
      "machine_id": 612,
      "equipment_id": 314,
      "place": "Recepção 2",
      "cash_mode": "cash_and_cashless",
      "restock_mode": "restock_and_cash_collect",
      "notifications_enabled": false
    }
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
404         máquina não encontrada                { "status": "404", "error": "Not Found" }
422         erro ao atualizar                     ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao atualizar

::

  {
    "asset_number": [
      "não pode ficar em branco"
    ]
  }

Excluir
=======

::

  DELETE /api/v1/machines/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da máquina    sim
=========  ===============  ===========

Retorno
-------

======  ====================  =============
status  descrição             response body
======  ====================  =============
204     Excluído com sucesso  (vazio)
======  ====================  =============


Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
404         máquina não encontrada                { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================
