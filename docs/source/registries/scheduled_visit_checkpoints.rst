###########
Checkpoints
###########

Ver
===

::

  GET /api/v1/scheduled_visit_checkpoints/[id]

Parâmetros de URL:
------------------

==========  ================  ===========
parâmetro   descrição         obrigatório
==========  ================  ===========
id          id do checkpoint  sim
==========  ================  ===========

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ com os seguintes
campos:

* **id**: o id do checkpoint

* **scheduled_visit_id**: a data em que o checkpoint foi criado

* **created_at**: a data de criação do checkpoint

* **updated_at**: a data de atualização do checkpoint

* **restock**: se é um reabastecimento

* **cash_collect**: se é uma coleta

* **only_visit**: se não é nem um reabastecimento nem uma coleta, apenas uma visita

* **finished**: se está finalizado

* **finished_at**: a data em que o checkpoint foi finalizado

* **reopened_at**: a data em que o checkpoint foi reaberto

* **installation_id**: o id da instalação

* **planogram_id**: o id do planograma

* **pick_list_id**: o id da pick list

* **synched_at**: a data em que o checkpoint foi sincronizado com o VMpay
  Visitor

* **pending_inventory_adjustment**: se o ajuste de inventário está pendente

* **inventory_adjustment_id**: o id do ajuste de inventário

* **scheduled_at**: a data em que o agendamento foi efetuado

* **synched_by**: identificação do smartphone usado para sincronizar com o VMpay

* **edited_by**: identificação do usuário que editou a agenda

* **inventories**: lista de inventários em que cada elemento contém os seguintes
  campos:

  - **planogram_item_id**: o id do item do planograma

  - **capacity**: capacidade do item do planograma

  - **expected_vacant_amount**: saldo esperado para o item

  - **entered_vacant_amount**: saldo informado para o item no VMpay Visitor

  - **returned_amounts**: lista de retornos do Visitor com os seguintes campos:

    + **id**: o id do registro

    + **original_value**: valor do registro antes da edição

    + **value**: valor final após edição

    + **edited**: se o registro foi editado ou não

    + **code**: codigo do registro

      * **damaged_item_return**
      * **expired_item_return**
      * **grid_replacement_leftover**
      * **pick_list_leftover**
      * **technical_problem_return**
      * **incorrect_grid_return**
      * **relocated_machine_return**
      * **removed_machine_return**
      * **product_inversion_return**
      * **item_not_shipped_return**
      * **quantity_leftover**
      * **par_level_reduction**
      * **about_to_expire**

    + **description**: descrição do registro

      * **Retorno Danificado**
      * **Retorno Vencido**
      * **Retorno Troca de Grade**
      * **Retorno Pick list**
      * **Retorno Problema Técnico**
      * **Retorno Grade Incorreta**
      * **Retorno Máquina Remanejada**
      * **Retorno Máquina Retirada**
      * **Retorno Inversão Produto**
      * **Retorno Item não enviado**
      * **Retorno Excesso**
      * **Retorno Redução de Nível de par**
      * **Retorno A Vencer**

* **custom_values**: lista de campos customizados em que cada elemento contém os
  seguintes campos:

  - **field**: dados do campo customizado:

    + **name**: nome do campo

    + **label**: rótulo do campo

    + **required**: se o campo é obrigatório

    + **field_type**: tipo do campo

  - **field_value**:

    + **value**: valor preenchido no VMpay Visitor

Exemplo:

::

  {
    "id": 21013,
    "scheduled_visit_id": 4744,
    "created_at": "2016-12-21T07:56:05.000-02:00",
    "updated_at": "2016-12-21T10:16:01.000-02:00",
    "restock": true,
    "cash_collect": false,
    "only_visit": false,
    "finished": true,
    "finished_at": "2016-12-21T16:39:20.000-02:00",
    "reopened_at": null,
    "installation_id": 1896,
    "planogram_id": 11204,
    "pick_list_id": 63089,
    "synched_at": "2016-12-22T08:05:33.000-02:00",
    "pending_inventory_adjustment": true,
    "inventory_adjustment_id": null,
    "scheduled_at": "2016-12-21T10:16:01.000-02:00",
    "synched_by": "VMVISITOR - JOSÉ",
    "edited_by": "Claudio da Silva",
    "inventories": [
      {
        "planogram_item_id": 385102,
        "capacity": 10.0,
        "expected_vacant_amount": 6.0,
        "entered_vacant_amount": 7.0,
        "returned_amounts": [
          {
            "id": 15197,
            "original_value": 1.0,
            "value": 2.0,
            "edited": true,
            "code": "relocated_machine_return",
            "description": "Retorno Máquina Remanejada"
          }
        ]
      },
      {
        "planogram_item_id": 385103,
        "capacity": 10.0,
        "expected_vacant_amount": 0.0,
        "entered_vacant_amount": 0.0,
        "returned_amounts": []
      },
      {
        "planogram_item_id": 385104,
        "capacity": 13.0,
        "expected_vacant_amount": 5.0,
        "entered_vacant_amount": 2.0,
        "returned_amounts": [
          {
            "id": 15196,
            "original_value": 4.0,
            "value": 8.0,
            "edited": true,
            "code": "item_not_shipped_return",
            "description": "Retorno Item não enviado"
          }
        ]
      },
      {
        "planogram_item_id": 385105,
        "capacity": 10.0,
        "expected_vacant_amount": 0.0,
        "entered_vacant_amount": 8.0,
        "returned_amounts": [
          {
            "id": 15194,
            "original_value": 1.0,
            "value": 2.0,
            "edited": true,
            "code": "incorrect_grid_return",
            "description": "Retorno Grade Incorreta"
          },
          {
            "id": 15195,
            "original_value": 3.0,
            "value": 6.0,
            "edited": true,
            "code": "product_inversion_return",
            "description": "Retorno Inversão Produto"
          }
        ]
      }
    ],
    "custom_values": [
      {
        "field": {
          "name": "limpeza",
          "label": "Limpeza?",
          "field_type": "boolean",
          "required": true
        },
        "field_value": {
          "value": true
        }
      },
      {
        "field": {
          "name": "malote",
          "label": "Malote",
          "field_type": "string",
          "required": true
        },
        "field_value": {
          "value": "123"
        }
      }
    ]
  }
