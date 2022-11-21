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

  - **manual_entered_amount**: valor informado na correção manual

  - **vacant_amount_difference**: resultado do cálculo da diferença
    
    + **Positivo**: diferença resultou em quebra
    + **Negativo**: diferença resultou em sobra
    
  - **good_id**: o id do produto

  - **upc_code**: código do produto

  - **desired_price**: valor do produto
  
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
    "id": 68885,
    "scheduled_visit_id": 11174,
    "created_at": "2017-09-19T14:34:55.000Z",
    "updated_at": "2017-09-19T14:43:47.000Z",
    "restock": true,
    "cash_collect": false,
    "only_visit": false,
    "finished": true,
    "finished_at": "2017-09-19T14:42:39.000Z",
    "reopened_at": null,
    "installation_id": 4956,
    "planogram_id": 20618,
    "pick_list_id": 175126,
    "synched_at": "2017-09-19T14:42:39.000Z",
    "pending_inventory_adjustment": false,
    "inventory_adjustment_id": 90217,
    "scheduled_at": "2017-09-19T14:35:00.000Z",
    "synched_by": "Treinamento Fast",
    "edited_by": "",
    "inventories": [
        {
            "planogram_item_id": 912759,
            "capacity": 10.0,
            "expected_vacant_amount": 2.0,
            "entered_vacant_amount": 2.0,
            "manual_entered_amount": 0,
            "vacant_amount_difference": 0.0,
            "good_id": 2,
            "upc_code": "2",
            "desired_price": 2.0,
            "returned_amounts": []
        },
        {
            "planogram_item_id": 912760,
            "capacity": 10.0,
            "expected_vacant_amount": 2.0,
            "entered_vacant_amount": 2.0,
            "manual_entered_amount": 0,
            "vacant_amount_difference": -2.0,
            "good_id": 1,
            "upc_code": "1",
            "desired_price": 2.0,
            "returned_amounts": [
                {
                    "id": 15210,
                    "original_value": null,
                    "value": 2.0,
                    "edited": false,
                    "code": "expired_item_return",
                    "description": "Retorno Vencido"
                }
            ]
        },
        {
            "planogram_item_id": 912761,
            "capacity": 10.0,
            "expected_vacant_amount": 1.0,
            "entered_vacant_amount": 1.0,
            "manual_entered_amount": 0,
            "vacant_amount_difference": -1.0,
            "good_id": 1,
            "upc_code": "1",
            "desired_price": 2.0,
            "returned_amounts": [
                {
                    "id": 15212,
                    "original_value": null,
                    "value": 1.0,
                    "edited": false,
                    "code": "damaged_item_return",
                    "description": "Retorno Danificado"
                }
            ]
        }
    ],
    "custom_values": []
}
