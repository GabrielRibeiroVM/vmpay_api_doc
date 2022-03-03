#####################
Produtos fracionáveis
#####################

Listar
======

::

  GET /api/v1/fractionable_products

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
      "name": "Iscas de frango",
      "upc_code": "00001",
      "barcode": "20000001",
      "external_id": null,
      "weight": null,
      "tags": ["tag1", "tag2"],
      "cost_price": 1.23,
      "additional_barcodes": [],
      "unit": {
        "id": 2,
        "fractionable": true,
        "name": "gram",
        "conversion_factor": 1000
      },
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation": {
        "id": 78,
        "name": "CFOP: 5102; CSOSN: 102"
      },
      "url": "http://localhost:4000/api/v1/fractionable_products/163"
    },
    {
      "id": 164,
      "created_at": "2014-10-17T14:50:50.000-03:00",
      "updated_at": "2014-10-17T14:50:50.000-03:00",
      "type": "Product",
      "manufacturer_id": 56,
      "category_id": 23,
      "name": "Carne moída",
      "upc_code": "100",
      "barcode": "2000100",
      "external_id": null,
      "weight": null,
      "tags": ["tag2", "tag3"],
      "cost_price": null,
      "additional_barcodes": [
        { "id": 123, "value": "2000101" },
        { "id": 321, "value": "2000102" }
      ],
      "unit": {
        "id": 2,
        "fractionable": true,
        "name": "gram",
        "conversion_factor": 1000
      },
      "url": "http://localhost:4000/api/v1/fractionable_products/164"
    },
    {
      "id": 165,
      "created_at": "2014-10-17T14:51:30.000-03:00",
      "updated_at": "2014-10-17T14:51:30.000-03:00",
      "type": "Product",
      "manufacturer_id": 56,
      "category_id": 23,
      "name": "Picanha premium",
      "upc_code": "00003",
      "barcode": 20000003,
      "external_id": null,
      "weight": null,
      "tags": ["tag1", "tag3"],
      "cost_price": null,
      "additional_barcodes": [],
      "unit": {
        "id": 2,
        "fractionable": true,
        "name": "gram",
        "conversion_factor": 1000
      },
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation": {
        "id": 78,
        "name": "CFOP: 5102; CSOSN: 102"
      },
      "url": "http://localhost:4000/api/v1/fractionable_products/165"
    }
  ]

Ver
===

::

  GET /api/v1/fractionable_products/[id]

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
    "name": "Iscas de frango",
    "upc_code": "00001",
    "barcode": "20000001",
    "external_id": null,
    "weight": null,
    "cost_price": 1.23,
    "tags": ["tag1", "tag2"],
    "additional_barcodes": [],
    "unit": {
      "id": 2,
      "fractionable": true,
      "name": "gram",
      "conversion_factor": 1000
    },
    "ncm_code": "21069090",
    "cest_code": "1234567",
    "tax_operation": {
      "id": 78,
      "name": "CFOP: 5102; CSOSN: 102"
    },
    "url": "http://localhost:4000/api/v1/fractionable_products/163"
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

  POST /api/v1/fractionable_products

Request::

  {
    "product": {
      "type": "Product",
      "name": "Coxão mole",
      "manufacturer_id": 56,
      "category_id": 21,
      "unit_id": 2,
      "upc_code": 00005,
      "barcode": "20000005",
      "external_id": "123qwe",
      "weight": 123,
      "ncm_code": "21069090",
      "cest_code": "1234567",
      "tax_operation_id": 78,
      "cost_price": 1.23,
      "tags": ["tag1", "tag2"],
      "additional_barcodes_attributes": [
        { "value": "20000006" },
        { "value": "20000007" }
      ]
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
  * *unit_id*: id da unidade de medida.

Opcionais
^^^^^^^^^

* *product*

  * *upc_code*: código do produto.
  * *barcode*: código de barras do produto, a ser utilizado no micro market.
  * *external_id*: identificador externo do produto.
  * *weight*: peso do produto (em gramas)
  * *tags*: array com tags.
  * *cost_price*: preço de custo
  * *additional_barcodes_attributes*: Array com códigos de barras adicionais.

    * *value*: o código de barras.

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
    "name": "Coxão mole",
    "upc_code": "00005",
    "barcode": "20000005",
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
      { "id": 123, "value": "20000006" },
      { "id": 321, "value": "20000007" }
    ],
    "unit": {
      "id": 2,
      "fractionable": true,
      "name": "gram",
      "conversion_factor": 1000
    },
    "url": "http://localhost:4000/api/v1/fractionable_products/2830"
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

  {
    "unit": [
      "não é fracionável"
    ]
  }


Atualizar
=========

::

  PATCH /api/v1/fractionable_products/[id]

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
      "name": "Carne moída"
    }
  }

Campos
------

Ao menos um campo interno a *product* deve ser passado.

Caso se deseje remover um *additional_barcode*, deve-se adicionar o atributo
*_destroy* com valor *true* à chamada como no exemplo abaixo::

  {
    "product": {
      "name": "Carne moída",
      "tags": ["tag1", "tag2"],
      "additional_barcodes_attributes": [
        {
          "id": 123,
          "_destroy": true
        }
      ]
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
    "created_at": "2016-02-16T10:20:11.018-02:00",
    "updated_at": "2016-02-16T10:20:11.018-02:00",
    "type": "Product",
    "manufacturer_id": 56,
    "category_id": 21,
    "name": "Carne moída",
    "upc_code": "00005",
    "barcode": "20000005",
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
      { "id": 321, "value": "20000007" }
    ],
    "unit": {
      "id": 2,
      "fractionable": true,
      "name": "gram",
      "conversion_factor": 1000
    },
    "url": "http://localhost:4000/api/v1/fractionable_products/2830"
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

  DELETE /api/v1/fractionable_products/[id]

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
