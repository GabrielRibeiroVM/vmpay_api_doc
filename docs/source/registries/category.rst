##########
Categorias
##########

Listar
======

::

  GET /api/v1/categories

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
      "id": 199,
      "name": "Bebidas",
      "over18": false
    },
    {
      "id": 200,
      "name": "Doces",
      "over18": false
    },
    {
      "id": 201,
      "name": "Salgados",
      "over18": false
    },
    {
      "id": 208,
      "name": "Combo Promocional",
      "over18": false
    },
    {
      "id": 235,
      "name": "Barras de Cereal",
      "over18": false
    },
    {
      "id": 236,
      "name": "Achocolatados",
      "over18": false
    },
    {
      "id": 237,
      "name": "Sucos ",
      "over18": false
    },
    {
      "id": 238,
      "name": "Água Mineral",
      "over18": false
    },
    {
      "id": 239,
      "name": "Higiene e Limpeza",
      "over18": false
    },
    {
      "id": 252,
      "name": "Livros",
      "over18": false
    },
    {
      "id": 363,
      "name": "Picolés",
      "over18": false
    },
    {
      "id": 470,
      "name": "Insumos solúveis",
      "over18": false
    },
    {
      "id": 471,
      "name": "Cafés solúveis",
      "over18": false
    }
  ]

Ver
===

::

  GET /api/v1/categories/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da categoria  sim
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
    "id": 236,
    "name": "Achocolatados",
    "over18": false
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         categoria não encontrada  { "status": "404", "error": "Not Found" }
==========  ========================  =========================================

Criar
=====

::

  POST /api/v1/categories

Request::

  {
    "category": {
      "name": "Nome da Categoria",
      "over18": true
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *machine*

  * *name*: nome da categoria.
  * *over18*: indica se a categoria é restrita a maiores de idade.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 1,
    "name": "Nome da Categoria",
    "over18": true
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
    "name": [
      "não pode ficar em branco"
    ],
    "name": [
      "já está em uso"
    ]
  }

Atualizar
=========

::

  PATCH /api/v1/categories/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da categoria    sim
=========  ===============  ===========

Request::

  {
    "category": {
      "name": "Nome da Categoria Alterado"
    }
  }

Campos
------

Ao menos um campo interno a *category* deve ser passado.

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo::

  {
    "id": 1,
    "name": "Nome da categoria",
    "over18": false
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
404         categoria não encontrada                { "status": "404", "error": "Not Found" }
422         erro ao atualizar                     ver exemplo abaixo
==========  ====================================  ====================================================

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

  DELETE /api/v1/categories/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da categoria    sim
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
404         categoria não encontrada                { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================
