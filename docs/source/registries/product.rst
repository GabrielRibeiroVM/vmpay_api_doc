########
Produtos
########

Listar
======

::

  GET /api/v1/products

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **include_deleted**: indica se deseja incluir no retorno os produtos excluídos. (true/false)

  * Se não for informado, será considerado false como padrão.

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
      "id": 163,
      "created_at": "2014-10-17T14:50:15.000-03:00",
      "updated_at": "2014-10-17T14:50:15.000-03:00",
      "type": "Product",
      "manufacturer_id": 56,
      "category_id": 23,
      "name": "Ruffles 50 g",
      "upc_code": "91",
      "barcode": "1234567890",
      "external_id": null,
      "weight": null,
      "vendible_balance": -6.0,
      "tags": ["tag1", "tag2"],
      "cost_price": 1.23,
      "additional_barcodes": [],
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation": {
        "id": 78,
        "name": "CFOP: 5102; CSOSN: 102"
      },
      "url": "http://localhost:4000/api/v1/products/163",
      "inventories": [
        {
          "distribution_center_id": 1,
          "total_quantity": -16.0,
          "committed_quantity": 0.0
        }
      ]
    },
    {
      "id": 164,
      "created_at": "2014-10-17T14:50:50.000-03:00",
      "updated_at": "2014-10-17T14:50:50.000-03:00",
      "type": "Product",
      "manufacturer_id": 56,
      "category_id": 23,
      "name": "Doritos 55 g",
      "upc_code": "110",
      "barcode": "0987654321",
      "external_id": null,
      "weight": null,
      "vendible_balance": -6.0,
      "tags": ["tag2", "tag3"],
      "cost_price": null,
      "additional_barcodes": [
        { "id": 123, "value": "10191817" },
        { "id": 321, "value": "16151413" }
      ],
      "url": "http://localhost:4000/api/v1/products/164",
      "inventories": []
    },
    {
      "id": 165,
      "created_at": "2014-10-17T14:51:30.000-03:00",
      "updated_at": "2014-10-17T14:51:30.000-03:00",
      "type": "Product",
      "manufacturer_id": 56,
      "category_id": 23,
      "name": "Torcida Queijo 50 g",
      "upc_code": "93",
      "barcode": null,
      "external_id": null,
      "weight": null,
      "vendible_balance": -6.0,
      "tags": ["tag1", "tag3"],
      "deleted_at": "2014-12-17T14:51:30.000-03:00",
      "cost_price": null,
      "additional_barcodes": [],
      "packing": {
        "id":15,
        "name": "Caixa com 10 unidades",
        "quantity":10
      },
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation": {
        "id": 78,
        "name": "CFOP: 5102; CSOSN: 102"
      },
      "url": "http://localhost:4000/api/v1/products/165",
      "inventories": []
    }
  ]

Ver
===

::

  GET /api/v1/products/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do produto    sim
=========  ===============  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  {
    "id": 163,
    "created_at": "2014-10-17T14:50:15.000-03:00",
    "updated_at": "2014-10-17T14:50:15.000-03:00",
    "type": "Product",
    "manufacturer_id": 56,
    "category_id": 23,
    "name": "Ruffles 50 g",
    "upc_code": "91",
    "barcode": "1234567890",
    "external_id": null,
    "weight": null,
    "vendible_balance": -6.0,
    "tags": ["tag1", "tag2"],
    "cost_price": 1.23,
    "additional_barcodes": [],
    "ncm_code": "21069090",
    "cest_code": "1234567",
    "tax_operation": {
      "id": 78,
      "name": "CFOP: 5102; CSOSN: 102"
    },
    "url": "http://localhost:4000/api/v1/products/163",
    "inventories": []
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         produto não encontrado    { "status": "404", "error": "Not Found" }
==========  ========================  =========================================

Criar
=====

::

  POST /api/v1/products

Request::

  {
    "product": {
      "type": "Product",
      "name": "Schweppes Citrus",
      "manufacturer_id": 56,
      "category_id": 21,
      "upc_code": 111,
      "barcode": "1234567891",
      "external_id": "123qwe",
      "weight": 123,
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation_id": 78,
      "cost_price": 1.23,
      "tags": ["tag1", "tag2"],
      "additional_barcodes_attributes": [
        { "value": "10191817" },
        { "value": "16151413" }
      ],
      "good_packing_attributes": {
        "packing_id": 15
      }
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *product*

  * *name*: nome do produto.
  * *manufacturer_id*: id do fabricante.
  * *category_id*: id da categoria.

Opcionais
^^^^^^^^^

* *product*

  * *upc_code*: código do produto.
  * *barcode*: código de barras do produto, a ser utilizado no micro market.
  * *external_id*: identificador externo do produto.
  * *weight*: peso do produto (em gramas)
  * *cost_price*: preço de custo
  * *tags*: array com tags.
  * *additional_barcodes_attributes*: Array com códigos de barras adicionais.

    * *value*: o código de barras.

  * *good_packing_attributes*: Array com atributos do packing associado.

    * *packing_id*: Id do packing associado ao insumo. É necessário que o packing tenha "default"(Unidade) como unidade de medida, caso contrário ele é ignorado.

  * *ncm_code*: código ncm do produto.
  * *cest_code*: código cest do produto.
  * *tax_operation_id*: id da operação fiscal.

Retorno

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 2830,
    "created_at": "2016-02-16T10:20:11.018-02:00",
    "updated_at": "2016-02-16T10:20:11.018-02:00",
    "type": "Product",
    "manufacturer_id": 56,
    "category_id": 21,
    "name": "Schweppes Citrus",
    "upc_code": "111",
    "barcode": "1234567891",
    "external_id": "123qwe",
    "weight": 123,
    "tags": ["tag1", "tag2"],
    "ncm_code": "21069090",
    "cest_code": "1234567",
    "tax_operation": {
      "id": 78,
      "name": "CFOP: 5102; CSOSN: 102"
    },
    "cost_price": 1.23,
    "additional_barcodes": [
      { "id": 123, "value": "10191817" },
      { "id": 321, "value": "16151413" }
    ],
    "packing": {
      "id":15,
      "name": "Caixa com 10 unidades",
      "quantity":10
    },
    "url": "http://localhost:4000/api/v1/products/2830"
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
      "já está em uso"
    ]
  }


Atualizar
=========

::

  PATCH /api/v1/products/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do produto    sim
=========  ===============  ===========

Request::

  {
    "product": {
      "name": "Schweppes Guaraná"
    }
  }

Campos
------

Ao menos um campo interno a *product* deve ser passado.

Caso se deseje remover um *additional_barcode*, deve-se adicionar o atributo
*_destroy* com valor *true* à chamada como no exemplo abaixo::

  {
    "product": {
      "name": "Schweppes Guaraná",
      "tags": ["tag1", "tag2"],
      "additional_barcodes_attributes": [
        {
          "id": 123,
          "_destroy": true
        }
      ]
    }
  }

O mesmo vale para o *packing*::

  {
    "product": {
      "name": "Schweppes Guaraná",
      "tags": ["tag1", "tag2"],
      "good_packing_attributes": {
        "id": 15,
        "_destroy": true
      }
    }
  }

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo::

  {
    "id": 2830,
    "created_at": "2016-02-16T10:20:11.000-02:00",
    "updated_at": "2016-02-16T10:27:07.000-02:00",
    "type": "Product",
    "manufacturer_id": 56,
    "category_id": 21,
    "name": "Schweppes Guaraná",
    "upc_code": "111",
    "barcode": "1234567891",
    "external_id": null,
    "weight": null,
    "tags": ["tag1", "tag2"],
    "ncm_code": "21069090",
    "cest_code": "1234567",
    "tax_operation": {
      "id": 78,
      "name": "CFOP: 5102; CSOSN: 102"
    },
    "cost_price": 1.23,
    "additional_barcodes": [
      { "id": 123, "value": "10191817" },
      { "id": 321, "value": "16151413" }
    ],
    "packing": {
      "id":15,
      "name": "Caixa com 10 unidades",
      "quantity":10
    },
    "url": "http://localhost:4000/api/v1/products/2830"
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
404         produto não encontrado                { "status": "404", "error": "Not Found" }
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

  DELETE /api/v1/products/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do produto    sim
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
404         produto não encontrado                { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================

API obsoleta
============

A API abaixo tornou-se obsoleta em favor de uma API mais simples, documentada acima. A API abaixo ainda funciona, mas o seu uso é desencorajado.

Listar (obsoleto)
-----------------

::

    GET /api/v1/vendibles

Ver (obsoleto)
--------------

::

    GET /api/v1/vendibles/[id]

Criar (obsoleto)
----------------

::

    POST /api/v1/vendibles

Request::

    {
      "vendible": {
        "type": "Product",
        "name": "Vanilla Coke",
        "manufacturer_id": 56,
        "category_id": 21,
        "upc_code": 111
      }
    }

Campos
^^^^^^

Obrigatórios
^^^^^^^^^^^^

* *vendible*

  * *name*: nome do produto.
  * *type*: valor deve ser sempre *Product*.
  * *manufacturer_id*: id do fabricante.
  * *category_id*: id da categoria.

Opcionais
^^^^^^^^^

* *vendible*

  * *upc_code*: código do produto.
  * *good_packing_attributes*: Array com atributos do packing associado

    * *packing_id*: Id do packing associado ao insumo. É necessário que o packing tenha "default"(Unidade) como unidade de medida, caso contrário ele é ignorado.


Atualizar (obsoleto)
--------------------

::

    PATCH /api/v1/vendibles/[id]

Request::

    {
      "vendible": {
        "name": "New Vanilla Coke",
        "manufacturer_id": 521
      }
    }

Campos
^^^^^^

Ao menos um campo interno a *vendible* deve ser passado.

O parâmetro *type* é ignorado.

Excluir (obsoleto)
------------------

::

    DELETE /api/v1/vendibles/[id]
