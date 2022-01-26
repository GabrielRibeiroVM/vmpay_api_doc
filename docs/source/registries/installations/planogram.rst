###########
Planogramas
###########

Listar
======

Lista os planogramas de determinada máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/planograms

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
===============  ================  ===========

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
      "id": 2477,
      "created_at": "2015-11-04T11:11:02.000-02:00",
      "updated_at": "2015-11-12T15:46:32.000-02:00",
      "due": "due_now",
      "started_at": "2015-11-04T11:12:02.000-02:00",
      "ended_at": "2015-11-12T15:41:52.000-02:00",
      "details": "Planograma temporário",
      "items": [
        {
          "id": 93477,
          "created_at": "2015-11-04T11:11:02.000-02:00",
          "updated_at": "2015-12-21T09:35:15.000-02:00",
          "planogram_id": 2477,
          "type": "Coil",
          "good_id": 163,
          "name": "11",
          "capacity": 8,
          "par_level": 8,
          "alert_level": 3,
          "desired_price": 4.5,
          "modified": false,
          "undefined": false,
          "logical_locator": "1",
          "physical_locators": [
            "11"
          ],
          "children": null,
          "current_balance": 6,
          "status": "active",
          "good": {
            "id": 163,
            "name": "Ruffles 50 g",
            "upc_code": "91",
            "upc_code_name": "91 - Ruffles 50 g",
            "unit_description": "Unidade",
            "unit_symbol": "un"
          }
        },
        {
          "id": 93478,
          "created_at": "2015-11-04T11:11:02.000-02:00",
          "updated_at": "2015-12-21T09:35:15.000-02:00",
          "planogram_id": 2477,
          "type": "Coil",
          "good_id": 1449,
          "name": "12",
          "capacity": 8,
          "par_level": 8,
          "alert_level": 3,
          "desired_price": 2.75,
          "modified": false,
          "undefined": false,
          "logical_locator": "2",
          "physical_locators": [
            "12"
          ],
          "children": null,
          "current_balance": 5,
          "status": "active",
          "good": {
            "id": 1449,
            "name": "Rosquiletas",
            "upc_code": "232",
            "upc_code_name": "232 - Rosquiletas",
            "unit_description": "Unidade",
            "unit_symbol": "un"
          }
        }
      ]
    }
  ]

Ver
===

Mostra determinado planograma de uma máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/planograms/[id]

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id do planograma  sim
===============  ================  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  {
    "id": 189976,
    "created_at": "2016-01-26T17:36:44.000-02:00",
    "updated_at": "2016-01-26T17:36:44.000-02:00",
    "due": "now",
    "started_at": "2016-01-26T17:36:44.000-02:00",
    "details": "Planograma temporário",
    "items": [
      {
        "id": 86717,
        "type": "Coil",
        "name": "1,2",
        "good_id": 10,
        "capacity": 20,
        "par_level": 20,
        "alert_level": 4,
        "desired_price": 2.5,
        "logical_locator": 1,
        "current_balance": 11.0,
        "status": "active",
      },
      {
        "id": 86718,
        "type": "Coil",
        "name": "3",
        "good_id": 12,
        "capacity": 10,
        "par_level": 10,
        "alert_level": 2,
        "desired_price": 2.3,
        "logical_locator": 2,
        "current_balance": 8.0,
        "status": "active",
      },
      {
        "id": 86719,
        "type": "VirtualCoil",
        "name": "4",
        "good_id": 23,
        "desired_price": 4.0,
        "logical_locator": 3,
        "children": { "1": 2, "2": 1 },
        "status": "active",
      },
      {
        "id": 86720,
        "type": "Canister",
        "good_id": 26,
        "capacity": 2000,
        "par_level": 2000,
        "alert_level": 200,
        "logical_locator": 4,
        "current_balance": 983.3,
        "status": "active",
      },
      {
        "id": 86721,
        "type": "Canister",
        "good_id": 27,
        "capacity": 3000,
        "par_level": 3000,
        "alert_level": 300,
        "logical_locator": 5,
        "current_balance": 1975.4,
        "status": "active",
      },
      {
        "id": 86722,
        "type": "VirtualCanister",
        "good_id": 30,
        "name": "5",
        "desired_price": 3.0,
        "logical_locator": 6,
        "children": { "4": 20, "5": 15 },
        "status": "active",
      }
    ]
  }

Erros
-----

======  ============================================  =========================================
status  descrição                                     response body
======  ============================================  =========================================
404     máquina/instalação/planograma não encontrado  { "status": "404", "error": "Not Found" }
======  ============================================  =========================================

Criar
=====

Cria uma novo planograma em determinada máquina e instalação.

O planograma criado fica pendente e pode ser atualizado. O mesmo só entra em atividade no próximo reabastecimento da máquina.

Uma instalação pode ter somente um planograma pendente. Se houver uma tentativa de cadastro de um outro planograma, será retornado um erro de validação, código HTTP 422.

::

  POST /api/v1/machines/[machine_id]/installations/[installation_id]/planograms

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
    "planogram": {
      "details": "Planograma para testes de canaleta",
      "items_attributes": [
        {
          "type": "Coil",
          "name": "1,2",
          "good_id": 10,
          "capacity": 20,
          "par_level": 20,
          "alert_level": 4,
          "desired_price": 2.5,
          "logical_locator": 1,
          "status": "active"
        },
        {
          "type": "Coil",
          "name": "3,4",
          "good_id": 11,
          "capacity": 20,
          "par_level": 20,
          "alert_level": 4,
          "desired_price": 2.5,
          "logical_locator": 2,
          "status": "active"
        },
        {
          "type": "Canister",
          "good_id": 12,
          "capacity": 3000,
          "par_level": 3000,
          "alert_level": 500,
          "logical_locator": 3
        },
        {
          "type": "Canister",
          "good_id": 13,
          "capacity": 300,
          "par_level": 300,
          "alert_level": 50,
          "logical_locator": 4
        },
        {
          "type": "VirtualCanister",
          "name": "5",
          "good_id": 15,
          "desired_price": 3.5,
          "logical_locator": 5,
          "children": { "3": 21, "4": 1 }
        },
        {
          "type": "VirtualCoil",
          "name": "6",
          "good_id": 23,
          "desired_price": 6.0,
          "logical_locator": 6,
          "children": { "1": 2, "2": 1 }
        }
      ]
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *planogram*

  * *items_attributes*: um array contendo os items do planograma (deve conter no máximo 2000 items, caso contrário o servidor poderá recusar a requisição).

    * Os items podem ser de 4 tipos: canaletas, combos, canisters e seleções.
    * Canaletas:

      * *type*: deve ser igual a "Coil".
      * *name*: o **número da canaleta**. Caso se trate de um agrupamento de canaletas, os números devem ser separados por vírgulas. Este campo será mapeado em um vetor no campo *physical_locators* como pode ser observado no exemplo de retorno.
      * *good_id*: id do produto. Nesse caso não pode ser composto. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *capacity*: a capacidade total da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui a capacidade total, somando-se todas as canaletas.
      * *par_level*: o nível de par da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui o nível de par total, somando-se todas as canaletas.
      * *alert_level*: o nível de alerta da canaleta.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico da canaleta. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado

    * Combos:

      * *type*: deve ser igual a "VirtualCoil".
      * *name*: o **número de seleção do combo**. Este campo será mapeado em um vetor no campo *physical_locators* como pode ser observado no exemplo de retorno.
      * *good_id*: id do produto. Nesse caso deve ser composto e com o *type* *Combo*. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico do combo. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado
      * *children*: as canaletas e suas quantidades que compõe o combo. É um objeto cujas chaves são identificadores lógicos (campo *logical_locator*) das canaletas e os valores as quantidades. No exemplo acima, o combo é composto de 2 produtos da canaleta cujo *name* é "1,2" - ou seja, canaletas 1 e 2 agrupadas - e 1 produto da canaleta cujo *name* é "3,4".

    * Canisters:

      * *type*: deve ser igual a "Canister".
      * *good_id*: id do insumo. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *capacity*: a capacidade total do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *par_level*: o nível de par do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *alert_level*: o nível de alerta do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *logical_locator*: trata-se do identificador lógico do canister. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado

    * Seleções:

      * *type*: deve ser igual a "VirtualCanister".
      * *name*: o **número da seleção**. Este campo será mapeado em um vetor no campo *physical_locators* como pode ser observado no exemplo de retorno.
      * *good_id*: id do produto. Nesse caso deve ser composto e com o *type* *Mixture*. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico da seleção. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado
      * *children*: os canisters e suas quantidades que compõe a seleção. É um objeto cujas chaves são identificadores lógicos (campo *logical_locator*) dos canisters e os valores as quantidades. No exemplo acima, digamos que o insumo de id 12 seja *Chocolate Solúvel com Leite* e o de id 13, *Copo Plástico 160 ml*. Logo, a seleção é composta de 21 gramas de Chocolate Solúvel com Leite e 1 unidade de Copo Plástico 160 ml.


    * Campo Status:

      - *active*: o item está ativo e disponível para uso no vmpay e para venda
      - *inactive*: o item está inativo e não poderá ser usado no vmpay nem disponibilizado para venda
      - *suspended* o item está suspenso e não poderá ser usado no vmpay, mas as unidades em campo poderão ser vendidas


Opcionais
^^^^^^^^^

* *planogram*

  - *details*: Texto explicativo relacionado ao planograma

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 2950,
    "created_at": "2016-02-15T16:19:36.843-02:00",
    "updated_at": "2016-02-15T16:19:36.843-02:00",
    "due": "due_next_restock",
    "started_at": null,
    "ended_at": null,
    "details": "Planograma para testes de canaleta",
    "items": [
      {
        "id": 113846,
        "created_at": "2016-02-15T16:19:36.843-02:00",
        "updated_at": "2016-02-15T16:19:36.843-02:00",
        "planogram_id": 2950,
        "type": "Coil",
        "good_id": 10,
        "name": "1,2",
        "capacity": 20,
        "par_level": 20,
        "alert_level": 4,
        "desired_price": 2.5,
        "modified": false,
        "undefined": false,
        "logical_locator": "1",
        "physical_locators": [
          "1",
          "2"
        ],
        "children": null,
        "current_balance": 0,
        "status": "active",
        "good": {
          "id": 10,
          "name": "Amendoin",
          "upc_code": "77",
          "upc_code_name": "77 - Amendoin",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      },
      {
        "id": 113847,
        "created_at": "2016-02-15T16:19:36.843-02:00",
        "updated_at": "2016-02-15T16:19:36.843-02:00",
        "planogram_id": 2950,
        "type": "Coil",
        "good_id": 11,
        "name": "3,4",
        "capacity": 20,
        "par_level": 20,
        "alert_level": 4,
        "desired_price": 2.5,
        "modified": false,
        "undefined": false,
        "logical_locator": "2",
        "physical_locators": [
          "3",
          "4"
        ],
        "children": null,
        "current_balance": 0,
        "status": "active",
        "good": {
          "id": 11,
          "name": "Coca Cola",
          "upc_code": "77",
          "upc_code_name": "77 - Coca Cola",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      },
      {
        "id":113848,
        "created_at":"2016-02-15T16:19:36.843-02:00",
        "updated_at":"2016-02-15T16:19:36.843-02:00",
        "planogram_id":2950,
        "type":"Canister",
        "good_id":12,
        "name":"Chocolate Solúvel com Leite 1kg",
        "capacity":3000.0,
        "par_level":3000.0,
        "alert_level":500.0,
        "desired_price":null,
        "modified": false,
        "undefined":false,
        "logical_locator":"3",
        "physical_locators":[],
        "children":null,
        "current_balance":0,
        "status": "active",
        "good":{
          "id":12,
          "name":"Chocolate Solúvel com Leite 1kg",
          "upc_code":null,
          "upc_code_name":"Chocolate Solúvel com Leite 1kg",
          "unit_description":"Grama",
          "unit_symbol":"g"
        }
      },
      {
        "id":113849,
        "created_at":"2016-02-15T16:19:36.843-02:00",
        "updated_at":"2016-02-15T16:19:36.843-02:00",
        "planogram_id":2950,
        "type":"Canister",
        "good_id":13,
        "name":"Copo Plástico 160 ml",
        "capacity":300.0,
        "par_level":300.0,
        "alert_level":50.0,
        "desired_price":null,
        "modified": false,
        "undefined":false,
        "logical_locator":"4",
        "physical_locators":[],
        "children":null,
        "current_balance":0,
        "status": "active",
        "good":{
          "id":13,
          "name":"Copo Plástico 160 ml",
          "upc_code":null,
          "upc_code_name":"Copo Plástico 160 ml",
          "unit_description":"Unidade",
          "unit_symbol":"un"
        }
      },
      {
        "id": 113850,
        "created_at": "2016-02-15T16:19:36.843-02:00",
        "updated_at": "2016-02-15T16:19:36.843-02:00",
        "planogram_id": 2950,
        "type": "VirtualCanister",
        "good_id": 15,
        "name": "5",
        "capacity": 10,
        "par_level": 10,
        "alert_level": 2,
        "desired_price": 3.5,
        "modified": false,
        "undefined": false,
        "logical_locator": "5",
        "physical_locators": [
          "5"
        ],
        "children": "children": {
          "3": "21.00",
          "4": "1.00"
        },
        "current_balance": 0,
        "status": "active",
        "good": {
          "id": 15,
          "name": "Dose Chocolate Quente",
          "upc_code": null,
          "upc_code_name": "Dose Chocolate Quente",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      },
      {
        "id": 113851,
        "created_at": "2016-02-15T16:19:36.843-02:00",
        "updated_at": "2016-02-15T16:19:36.843-02:00",
        "planogram_id": 2950,
        "type": "VirtualCoil",
        "good_id": 23,
        "name": "6",
        "capacity": 10,
        "par_level": 10,
        "alert_level": 4,
        "desired_price": 6,
        "modified": false,
        "undefined": false,
        "logical_locator": "6",
        "physical_locators": [
          "6"
        ],
        "children": {
          "1": "2.00",
          "2": "1.00"
        },
        "status": "active",
        "good": {
          "id": 23,
          "name": "2x Amendoins + 1x Coca Cola",
          "upc_code": "0",
          "upc_code_name": "0 - 2x Amendoins + 1x Coca Cola",
          "unit_description": "Unidade",
          "unit_symbol": "un"
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
401         não autorizado                        (vazio)
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "base": [
      "Já existe um planograma cadastrado para o próximo reabastecimento",
      "Há uma pick list pendente para essa instalação"
    ]
  }


Atualizar
=========

Atualiza um planograma de determinada máquina e instalação.

Somente planogramas pendentes podem ser atualizados. Se houver uma tentativa de atualização de planograma ativo ou anterior, será retornado um erro de validação, código HTTP 422.

::

  PATCH /api/v1/machines/[machine_id]/installations/[installation_id]/planograms/[id]

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id do planograma  sim
===============  ================  ===========

Request::

  {
    "planogram": {
      "details": "Planograma para testes de canaleta",
      "items_attributes": [
        {
          "id": 113846,
          "type": "Coil",
          "name": "1,2",
          "good_id": 10,
          "capacity": 25,
          "par_level": 25,
          "alert_level": 5,
          "desired_price": 2.5,
          "logical_locator": 1,
          "status": "active"
        }
      ]
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *planogram*

  * *items_attributes*: um array contendo os items do planograma (deve conter no máximo 2000 items, caso contrário o servidor poderá recusar a requisição).

    * Os items podem ser de 4 tipos: canaletas, combos, canisters e seleções.
    * Canaletas:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do planograma.
      * *type*: deve ser igual a "Coil".
      * *name*: o número da canaleta. Caso se trate de um agrupamento de canaletas, os números devem ser separados por vírgulas.
      * *good_id*: id do produto. Nesse caso não pode ser composto. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *capacity*: a capacidade total da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui a capacidade total, somando-se todas as canaletas.
      * *par_level*: o nível de par da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui o nível de par total, somando-se todas as canaletas.
      * *alert_level*: o nível de alerta da canaleta.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico da canaleta. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado

    * Combos:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do planograma.
      * *type*: deve ser igual a "VirtualCoil".
      * *name*: o número de seleção do combo.
      * *good_id*: id do produto. Nesse caso deve ser composto e com o *type* *Combo*. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico do combo. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado
      * *children*: as canaletas e suas quantidades que compõe o combo. É um objeto cujas chaves são identificares lógicos (campo *logical_locator*) das canaletas e os valores as quantidades. No exemplo acima, o combo é composto de 2 produtos da canaleta cujo *name* é "1,2" - ou seja, canaletas 1 e 2 agrupadas - e 1 produto da canaleta 3.

    * Canisters:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do planograma.
      * *type*: deve ser igual a "Canister".
      * *good_id*: id do insumo. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *capacity*: a capacidade total do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *par_level*: o nível de par do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *alert_level*: o nível de alerta do canister. Deve ser preenchido na mesma unidade do insumo (g, ml ou un).
      * *logical_locator*: trata-se do identificador lógico do canister. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado

    * Seleções:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do planograma.
      * *type*: deve ser igual a "VirtualCanister".
      * *name*: o número da seleção.
      * *good_id*: id do produto. Nesse caso deve ser composto e com o *type* *Mixture*. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico da seleção. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado
      * *children*: os canisters e suas quantidades que compõe a seleção. É um objeto cujas chaves são identificares lógicos (campo *logical_locator*) dos canisters e os valores as quantidades. No exemplo acima, digamos que o insumo de id 26 seja *Café em pó* e o de id 27, *Leite em pó*. Logo, a seleção é composta de 20 gramas de Café em pó e 15 gramas de Leite em pó.

    * Campo Status:

      - *active*: o item está ativo e disponível para uso no vmpay e para venda
      - *inactive*: o item está inativo e não poderá ser usado no vmpay nem disponibilizado para venda
      - *suspended* o item está suspenso e não poderá ser usado no vmpay, mas as unidades em campo poderão ser vendidas

Opcionais
^^^^^^^^^

* *planogram*

  - *details*: Texto explicativo relacionado ao planograma

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo:

::

  {
    "id": 2961,
    "created_at": "2016-02-16T16:54:39.000-02:00",
    "updated_at": "2016-02-16T16:54:39.000-02:00",
    "due": "due_next_restock",
    "started_at": null,
    "ended_at": null,
    "details": "Planograma para testes de canaleta",
    "items": [
      {
        "id": 113846,
        "created_at": "2016-02-16T16:54:39.000-02:00",
        "updated_at": "2016-02-16T17:03:27.727-02:00",
        "planogram_id": 2961,
        "type": "Coil",
        "good_id": 10,
        "name": "1,2",
        "capacity": 25,
        "par_level": 25,
        "alert_level": 5,
        "desired_price": 2.5,
        "modified": true,
        "undefined": false,
        "logical_locator": "1",
        "physical_locators": [
          "1",
          "2"
        ],
        "children": null,
        "current_balance": 0,
        "status": "active",
        "good": {
          "id": 10,
          "name": "Amendoin",
          "upc_code": "77",
          "upc_code_name": "77 - Amendoin",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      },
      {
        "id": 113847,
        "created_at": "2016-02-16T16:54:39.000-02:00",
        "updated_at": "2016-02-16T16:54:39.000-02:00",
        "planogram_id": 2961,
        "type": "Coil",
        "good_id": 12,
        "name": "3",
        "capacity": 10,
        "par_level": 10,
        "alert_level": 2,
        "desired_price": 2.3,
        "modified": true,
        "undefined": false,
        "logical_locator": "2",
        "physical_locators": [
          "3"
        ],
        "children": null,
        "current_balance": 0,
        "status": "active",
        "good": {
          "id": 12,
          "name": "Twix",
          "upc_code": "99",
          "upc_code_name": "99 - Twix",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      },
      {
        "id": 113848,
        "created_at": "2016-02-16T16:54:39.000-02:00",
        "updated_at": "2016-02-16T16:54:39.000-02:00",
        "planogram_id": 2961,
        "type": "VirtualCoil",
        "good_id": 23,
        "name": "4",
        "capacity": null,
        "par_level": null,
        "alert_level": null,
        "desired_price": 4,
        "modified": true,
        "undefined": false,
        "logical_locator": "3",
        "physical_locators": [
          "4"
        ],
        "children": {
          "1": 2,
          "2": 1
        },
        "status": "active",
        "good": {
          "id": 23,
          "name": "Camiseta Acqua tamanho G",
          "upc_code": "0",
          "upc_code_name": "0 - Camiseta Acqua tamanho G",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        }
      }
    ]
  }

Erros
-----

==========  ============================================  ==============================================
status      descrição                                     response body
==========  ============================================  ==============================================
400         parâmetros faltando                           { "status": "400", "error": "Bad Request" }
401         não autorizado                                (vazio)
404         máquina/instalação/planograma não encontrado  { "status": "404", "error": "Not Found" }
422         erro ao atualizar                             ver exemplo abaixo
==========  ============================================  ==============================================

422 - erro ao atualizar:

::

  {
    "items.physical_locators": [
      "já está em uso"
    ],
    "base": [
      "Registros filhos duplicados"
    ]
  }

Excluir
=======

Exclui um planograma de determinada máquina e instalação.

Somente planogramas pendentes podem ser excluídos. Se houver uma tentativa de exclusão de planograma ativo ou anterior, será retornado um erro de validação, código HTTP 422.

::

  DELETE /api/v1/machines/[machine_id]/installations/[installation_id]/planograms/[id]

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id do planograma  sim
===============  ================  ===========

Retorno
-------

======  ====================  =============
status  descrição             response body
======  ====================  =============
204     Excluído com sucesso  (vazio)
======  ====================  =============


Erros
-----

==========  ============================================  ===========================================
status      descrição                                     response body
==========  ============================================  ===========================================
404         máquina/instalação/planograma não encontrado  { "status": "404", "error": "Not Found" }
==========  ============================================  ===========================================
