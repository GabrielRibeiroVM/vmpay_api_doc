################
Planograma atual
################

Ver
===

Mostra o planograma atual de uma máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/current_planogram

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

Atualizar
=========

Atualiza o planograma atual de determinada máquina e instalação.

Algumas condições devem ser respeitadas:

* Somente planogramas de máquinas de micromarket podem ser atualizados.
* Não pode haver pick list pendente para ocorrer a atualização.
* Não é permitido alterar os campos *name*, *type*, *good_id*, *logical_locator* e *children* dos itens.
* Não é possível incluir ou alterar cânisters ou seleções.
* Não é possível excluir itens. O parâmetro *_destroy* será ignorado. Entretanto, um item pode ser suspenso ou inativado (ver abaixo).

Se as condições descritas não forem satisfeitas, será retornado um erro de validação, código HTTP 422.

É possível incluir itens novos, desde que não sejam cânisters ou seleções.

::

  PATCH /api/v1/machines/[machine_id]/installations/[installation_id]/current_planogram

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
          "id": 113846,
          "capacity": 25,
          "par_level": 25,
          "alert_level": 5,
          "desired_price": 6.5,
          "logical_locator": 1,
          "status": "active"
        },
        {
          "id": 113848,
          "desired_price": 4,
          "status": "suspended"
        },
        {
          "type": "Coil",
          "good_id": 12,
          "name": "4",
          "capacity": 10,
          "par_level": 10,
          "alert_level": 2,
          "desired_price": 2.3,
          "logical_locator": "4",
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

    * Os items podem ser de 2 tipos: canaletas e combos.
    * Canaletas:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do item.
      * *type*: deve ser igual a "Coil". Não pode ser alterado em itens já existentes.
      * *name*: o número da canaleta. Caso se trate de um agrupamento de canaletas, os números devem ser separados por vírgulas. Não pode ser alterado em itens já existentes.
      * *good_id*: id do produto. Nesse caso não pode ser composto. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_. Não pode ser alterado em itens já existentes.
      * *capacity*: a capacidade total da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui a capacidade total, somando-se todas as canaletas.
      * *par_level*: o nível de par da canaleta. No caso de agrupameto de canaletas, deve-se colocar aqui o nível de par total, somando-se todas as canaletas.
      * *alert_level*: o nível de alerta da canaleta.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico da canaleta. Deve-se gerar um inteiro único dentro de todos os items do planograma. Não pode ser alterado em itens já existentes.
      * *status*: o estado do item no planograma. Caso não seja informado em itens novos, o padrão *active* será usado.

    * Combos:

      * *id*: o id do item, gerado automaticamente pelo sistema no momento da criação do item.
      * *type*: deve ser igual a "VirtualCoil". Não pode ser alterado em itens já existentes.
      * *name*: o número de seleção do combo. Não pode ser alterado em itens já existentes.
      * *good_id*: id do produto. Nesse caso deve ser composto e com o *type* *Combo*. `Good <https://en.wikipedia.org/wiki/Good_%28economics%29>`_ neste caso se traduz como `bem <https://pt.wikipedia.org/wiki/Bem_%28economia%29>`_. Não pode ser alterado em itens já existentes.
      * *desired_price*: o preço unitário desejado.
      * *logical_locator*: trata-se do identificador lógico do combo. Deve-se gerar um inteiro único dentro de todos os items do planograma.
      * *status*: o estado do item no planograma. Caso não seja informado, o padrão *active* será usado.
      * *children*: as canaletas e suas quantidades que compõe o combo. É um objeto cujas chaves são identificares lógicos (campo *logical_locator*) das canaletas e os valores as quantidades. No exemplo acima, o combo é composto de 2 produtos da canaleta cujo *name* é "1,2" - ou seja, canaletas 1 e 2 agrupadas - e 1 produto da canaleta 3. Não pode ser alterado em itens já existentes.

    * Campo *status*:

      * *active*: o item está ativo e disponível para uso no vmpay e para venda.
      * *inactive*: o item está inativo e não poderá ser usado no vmpay nem disponibilizado para venda.
      * *suspended*: o item está suspenso e não poderá ser usado no vmpay, mas as unidades em campo poderão ser vendidas.

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
        "desired_price": 6.5,
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
        "status": "suspended",
        "good": {
          "id": 23,
          "name": "Camiseta Acqua tamanho G",
          "upc_code": "0",
          "upc_code_name": "0 - Camiseta Acqua tamanho G",
          "unit_description": "Unidade",
          "unit_symbol": "un"
        },
        {
          "id": 113849,
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
    "items.name": [
      "não pode mudar"
    ],
    "base": [
      "Registros filhos duplicados"
    ]
  }
