#######################
Centros de distribuição
#######################

Listar
======

::

  GET /api/v1/distribution_centers

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
       "name": "Padrão",
       "external_id": 123
     },
     {
       "id": 2,
       "name": "Estoque 2",
       "external_id": 124
     }
  ]

Erros
-----

==========  =============================  =========================================
status      descrição                      response body
==========  =============================  =========================================
401         não autorizado                 (vazio)
==========  =============================  =========================================

Ver
===

::

  GET /api/v1/distribution_centers/[id]

Parâmetros de URL:
------------------

=========  ============================  ===========
parâmetro  descrição                     obrigatório
=========  ============================  ===========
id         id do centro de distribuição   sim
=========  ============================  ===========

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
    "id": 1,
    "name": "Padrão",
    "external_id": 123
  }

Campos
------

* *name*: o nome do centro de distribuição.
* *external_id*: identificador externo do centro de distribuição a ser utilizado em integrações.

Erros
-----

======  =============================  =========================================
status  descrição                      response body
======  =============================  =========================================
401     não autorizado                 (vazio)
404     registro não encontrado        { "status": "404", "error": "Not Found" }
======  =============================  =========================================

Criar
=====

::

  POST /api/v1/distribution_centers

Request::

  {
    "distribution_center": {
      "name": "Estoque 3",
      "external_id": "125"
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *distribution_center*

  * *name*: o nome do centro de distribuição.

Opcionais
^^^^^^^^^

* *distribution_center*

  * *external_id*: identificador externo do centro de distribuição a ser utilizado em integrações.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     criado com sucesso
======  ==================

Exemplo::

  {
    "id": 3,
    "name": "Estoque 3",
    "external_id": 125
  }

Erros
-----

======  ==============================  ===========================================
status  descrição                       response body
======  ==============================  ===========================================
400     parâmetros faltando             { "status": "400", "error": "Bad Request" }
401     não autorizado                  (vazio)
422     erro ao criar                   ver exemplo abaixo
======  ==============================  ===========================================

422 - erro ao criar

::

  {
    "name": [
      "não pode ficar em branco"
    ],
    "external_id": [
      "já está em uso"
    ]
  }

Atualizar
=========

::

  PATCH /api/v1/distribution_centers/[id]

Parâmetros de URL:
------------------

=========  ============================  ===========
parâmetro  descrição                     obrigatório
=========  ============================  ===========
id         id do centro de distribuição   sim
=========  ============================  ===========

Request::

  {
    "distribution_center": {
      "name": "Estoque 2",
      "external_id": "125"
    }
  }

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  {
    "id": 2,
    "name": "Estoque 2",
    "external_id": 125
  }

Erros
-----

======  =============================  ===========================================
status  descrição                      response body
======  =============================  ===========================================
400     parâmetros faltando            { "status": "400", "error": "Bad Request" }
401     não autorizado                 (vazio)
404     registro não encontrado        { "status": "404", "error": "Not Found" }
422     erro ao atualizar              ver exemplo abaixo
======  =============================  ===========================================

422 - erro ao atualizar

::

  {
    "name": [
      "não pode ficar em branco"
    ]
  }

Excluir
=======

::

  DELETE /api/v1/distribution_centers/[id]

Parâmetros de URL:
------------------

=========  ============================  ===========
parâmetro  descrição                     obrigatório
=========  ============================  ===========
id         id do centro de distribuição   sim
=========  ============================  ===========

Retorno
-------

======  ====================  =============
status  descrição             response body
======  ====================  =============
204     excluído com sucesso  (vazio)
======  ====================  =============

Erros
-----

======  =============================  =========================================
status  descrição                      response body
======  =============================  =========================================
401     não autorizado                 (vazio)
404     registro não encontrado        { "status": "404", "error": "Not Found" }
======  =============================  =========================================
