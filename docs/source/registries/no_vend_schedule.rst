###################################
Agendamentos de alerta de não venda
###################################

Listar
======

::

  GET /api/v1/no_vend_schedules

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
      "id": 1,
      "created_at": "2020-09-23T16:17:17.000Z",
      "updated_at": "2020-09-23T16:17:17.000Z",
      "description": "Alerta padrão",
      "default": true
    }
  ]
