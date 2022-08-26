Integração com ERP
##################

Histórico de alterações
***********************

+------------+-----------------------------------------------------------------------+
| 2022-05-25 | - Versão inicial                                                      |
+------------+-----------------------------------------------------------------------+
| 2022-07-12 | - Limita número de itens no parâmetro *inventories* em                |
|            |   `Registrar evento <#service-vmpay-re>`_.                            |
|            | - Adiciona o parâmetro *nfe_key* ao evento de *confirmação de venda*. |
|            | - Adiciona o parâmetro *issues_nfe* ao serviço                        |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
|            | - Define as formas de pagamento possíveis em                          |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
+------------+-----------------------------------------------------------------------+
| 2022-07-18 | - Inclui formas de pagamento faltantes em                             |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
|            | - Exclui o parâmetro *issues_nfe* do serviço                          |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
|            | - Adiciona os parâmetro *price* e *quantity* ao serviço               |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
|            | - Atualiza o exemplo de request para melhor refletir tipos em         |
|            |   `Registrar venda <#service-erp-rv>`_.                               |
|            | - Corrige documentação em `Registrar venda <#service-erp-rv>`_: o     |
|            |   *price* em *items* trata-se do  preço **unitário**, e não do total  |
|            |   do item.                                                            |
+------------+-----------------------------------------------------------------------+
| 2022-07-18 | - Para deixar o intuito mais claro, foram renomeados alguns parâmetros|
|            |   em `Registrar venda <#service-erp-rv>`_: *price* -> *total_price*,  |
|            |   *quantity* -> *total_quantity*, *items.price* -> *items.unit_price*,|
|            |   *items.balance* -> *items.balance_after*.                           |
|            | - Adiciona os parâmetros *items.number*, *items.total_discount* e     |
|            |   *items.total_price* em `Registrar venda <#service-erp-rv>`_.        |
+------------+-----------------------------------------------------------------------+
| 2022-07-20 | - Para manter o padrão entre os serviços, os parâmetros de            |
|            |   `Ajustar estoques de máquina <#service-erp-aem>`_ foram indentados  |
|            |   dentro de *inventory_adjustment*.                                   |
+------------+-----------------------------------------------------------------------+
| 2022-07-21 | - Renomeia parâmetro *errors* para *erp_errors* em                    |
|            |   `Registrar evento <#service-vmpay-re>`_ (eventos *erro em           |
|            |   confirmação de pick list*, *erro em cancelamento de pick list* e    |
|            |   *erro em confirmação de venda*).                                    |
|            | - Adiciona os parâmetros *cnpj_authorizer*, *authorization_code* e    |
|            |   *card_brand* em `Registrar venda <#service-erp-rv>`_.               |
|            | - Correções diversas no texto da documentação.                        |
+------------+-----------------------------------------------------------------------+
| 2022-07-25 | - Muda nome de header *API-key* para *X-API-Key* em                   |
|            |   `Serviços implementados no ERP <#services-erp>`_.                   |
+------------+-----------------------------------------------------------------------+
| 2022-08-12 | - Documenta novo parâmetro *fatal_erp_error* em                       |
|            |   `Registrar evento <#service-vmpay-re>`_ (eventos *erro em           |
|            |   confirmação de pick list* e *erro em cancelamento de pick list*).   |
+------------+-----------------------------------------------------------------------+
| 2022-08-26 | - Documenta o serviço                                                 |
|            |   `Baixa de estoque de máquina <#service-erp-bem>`_ do ERP e os       |
|            |   eventos *retorno de estoque* e *erro de retorno de estoque* em      |
|            |   `Registrar evento <#service-vmpay-re>`_.                            |
|            | - Documenta erros do serviço                                          |
|            |   `Confirmar pick list <#service-erp-copl>`_.                         |
|            | - Muda os eventos de erro para serem eventos de log em                |
|            |   `Registrar evento <#service-vmpay-re>`_.                            |
+------------+-----------------------------------------------------------------------+

Introdução
**********

A integração entre o VMpay e um ERP se dá, principalmente, através da sincronização de estoques de centros de distribuição e máquinas. O responsável pela atualização dos estoques dos centros de distribuição fica sendo o ERP: o VMpay apenas replica os saldos informados. Da mesma maneira, o responsável por atualizar os estoques nas máquinas fica sendo o VMpay e o ERP apenas é informado quando isso ocorre - seja por vendas, ajustes ou qualquer outra operação.

Abaixo, o fluxo básico:

* O ERP informa a entrada de estoque de determinados produtos em algum centro de distribuição através da chamada do serviço `Registrar evento <#service-vmpay-re>`_ com o tipo *inventory_entry*. O *distribution_center_id* deve ser passado.
* O usuário cria uma pick list no VMpay, a qual fica pendente. O usuário pode editar várias vezes a pick list até ficar satisfeito com resultado.
* O usuário, então, libera a pick list e o serviço `Confirmar pick list <#service-erp-copl>`_ do ERP é chamado. O *pick_list_id* é passado como parâmetro. A pick list fica em estado de aguardando confirmação e, a partir deste momento, não pode ser mais editada.

  * Este serviço pode retornar erros de validação. Nesse caso, a pick list voltará a ficar pendente.

* O ERP faz as operações internas necessárias e, quando tudo estiver OK, chama o serviço `Registrar evento <#service-vmpay-re>`_ com o tipo *pick_list_confirmation*, informando também o *distribution_center_id*, o *pick_list_id*, os dados da nota fiscal de transporte e os novos saldos do centro de distribuição. A pick list é confirmada no VMpay.

  * Enquanto o evento de *confirmação de pick list* não for enviado, o ERP pode enviar vários eventos de log do tipo *pick_list_confirmation_log*. Estes podem ser somente uma notificação informativa (*log_level* igual a *information* ou *warning*) ou até algum erro (*log_level* igual a *error* ou *fatal*). Se o erro for fatal, a pick list será cancelada.

* Neste ponto o usuário pode cancelar a pick list, se encontrar algum problema. Se isso for feito, o serviço `Cancelar pick list <#service-erp-capl>`_ do ERP será chamado e a pick list ficará em estado de aguardando cancelamento.

  * Após o cancelamento no ERP, o serviço `Registrar evento <#service-vmpay-re>`_ é chamado novamente, agora com o tipo *pick_list_cancellation*. O *distribution_center_id*, o *pick_list_id* e os novos saldos do centro de distribuição também são passados. O VMpay, então, cancela a pick list.

    * Enquanto o evento de *cancelamento de pick list* não for enviado, o ERP pode enviar vários eventos de log do tipo *pick_list_cancellation_log*. Se o erro for fatal, a pick list voltará a ficar confirmada.

* Porém, se tudo estiver OK com a pick list, a mesma é posteriormente aplicada no VMpay. A partir deste momento o estoque na máquina é efetivamente atualizado no VMpay, o qual, então, chama o serviço `Aplicar pick list <#service-erp-apl>`_ do ERP.
* Quando ocorrer alguma venda no VMpay, o serviço `Registrar venda <#service-erp-rv>`_ do ERP é chamado com as informações da venda.

  * Após o processamento da venda no ERP, o serviço `Registrar evento <#service-vmpay-re>`_ é chamado com o tipo *sale_confirmation*, o *sale_id* e os dados da nota fiscal de venda.

    * Enquanto o evento de *confirmação de venda* não for enviado, o ERP pode enviar vários eventos de log do tipo *sale_confirmation_log*.

* Quando ocorrer um ajuste de estoque na máquina no VMpay, o serviço `Ajustar estoques de máquina <#service-erp-aem>`_ do ERP é chamado com as informações do que foi alterado.
* O ERP pode a qualquer momento fazer um ajuste de estoque no centro de distribuição. Quando isso ocorrer, o serviço `Registrar evento <#service-vmpay-re>`_ é chamado com o tipo *inventory_adjustment*.
* O ERP pode também fazer uma sincronização de estoque do centro de distribuição com o VMpay. Para tanto, o serviço `Registrar evento <#service-vmpay-re>`_ deve ser chamado com o tipo *inventory_synchronization*.
* Quando um ou mais produtos deixam de ser vendidos em uma máquina, o serviço `Baixa de estoque de máquina <#service-erp-bem>`_ do ERP é chamado com as informações dos produtos baixados e o seus saldos antes da baixa. Esses produtos devem ser movimentados de volta para o centro de distribuição. Para tanto, o ERP faz as operações necessárias e, depois, o serviço `Registrar evento <#service-vmpay-re>`_ é chamado com o tipo *inventory_return*, o *distribution_center_id*, o *machine_inventory_removal_id* e os novos saldos do centro de distribuição.

  * Enquanto o evento de *retorno de estque* não for enviado, o ERP pode enviar vários eventos de log do tipo *inventory_return_log*.

Serviços implementados no VMpay
*******************************

.. _service-vmpay-re:

Registrar evento
================

::

  POST /api/v1/erp/events

Este é o serviço principal de integração acessível ao ERP. Por ele registram-se os seguintes eventos: *entrada de estoque*, *confirmação de pick list*, *log de confirmação de pick list*, *cancelamento de pick list*, *log de cancelamento de pick list*, *confirmação de venda*, *log de confirmação de venda*, *ajuste de estoque*, *sincronização de estoque*, *retorno de estoque* e *log de retorno de estoque*.

Cada serviço possui um formato de payload diferente. Listamos um exemplo de cada abaixo.

Note que os eventos não são processados de forma síncrona. Por se tratar de operações potencialmente demoradas (especialmente as que atualizam muitos estoques), é sempre criado um job para que o evento seja processado em background. Logo, uma resposta bem sucedida apenas indica que o job foi criado.

Entrada de estoque::

  {
    "event": {
      "type": "inventory_entry",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "distribution_center_id": 1,
      "inventories": [
        {
          "storable_id": 123,
          "delta": -5,
          "balance": 115
        },
        {
          "storable_id": 321,
          "delta": -10,
          "balance": 90
        }
      ]
    }
  }

Confirmação de pick list::

  {
    "event": {
      "type": "pick_list_confirmation",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "pick_list_id": 12345,
      "transport_nfe_danfe_url": "https://site.com/1234.pdf",
      "transport_nfe_xml_url": "https://site.com/1234.xml",
      "inventories": [
        {
          "storable_id": 123,
          "delta": -5,
          "balance": 115
        },
        {
          "storable_id": 321,
          "delta": -10,
          "balance": 90
        }
      ]
    }
  }

Log de confirmação de pick list::

  {
    "event": {
      "type": "pick_list_confirmation_log",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "pick_list_id": 12345,
      "log_level": "fatal",
      "log_messages": [
        "Mensagem 1",
        "Mensagem 2"
      ]
    }
  }

Cancelamento de pick list::

  {
    "event": {
      "type": "pick_list_cancellation",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "pick_list_id": 12345,
      "inventories": [
        {
          "storable_id": 123,
          "delta": 5,
          "balance": 120
        },
        {
          "storable_id": 321,
          "delta": 10,
          "balance": 100
        }
      ]
    }
  }

Log de cancelamento de pick list::

  {
    "event": {
      "type": "pick_list_cancellation_log",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "pick_list_id": 12345,
      "log_level": "error",
      "log_messages": [
        "Mensagem 1",
        "Mensagem 2"
      ]
    }
  }

Confirmação de venda::

  {
    "event": {
      "type": "sale_confirmation",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "sale_id": 120934,
      "nfe_key": "12345",
      "nfe_danfe_url": "https://site.com/12345.pdf",
      "nfe_xml_url": "https://site.com/12345.xml",
    }
  }

Log de confirmação de venda::

  {
    "event": {
      "type": "sale_confirmation_log",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "sale_id": 120934,
      "log_level": "warning",
      "log_messages": [
        "Mensagem 1",
        "Mensagem 2"
      ]
    }
  }

Ajuste::

  {
    "event": {
      "type": "inventory_adjustment",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "distribution_center_id": 1,
      "inventories": [
        {
          "storable_id": 123,
          "delta": 5,
          "balance": 120
        },
        {
          "storable_id": 321,
          "delta": 10,
          "balance": 100
        }
      ]
    }
  }

Sincronização::

  {
    "event": {
      "type": "inventory_synchronization",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "distribution_center_id": 1,
      "inventories": [
        {
          "storable_id": 123,
          "balance": 120
        },
        {
          "storable_id": 321,
          "balance": 100
        }
      ]
    }
  }

Retorno de estoque::

  {
    "event": {
      "type": "inventory_return",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "distribution_center_id": 1,
      "machine_inventory_removal_id": 123,
      "inventories": [
        {
          "storable_id": 123,
          "delta": 10,
          "balance": 133
        },
        {
          "storable_id": 321,
          "delta": 10,
          "balance": 331
        }
      ]
    }
  }

Log de retorno estoque::

  {
    "event": {
      "type": "inventory_return_log",
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "distribution_center_id": 1,
      "machine_inventory_removal_id": 123,
      "log_level": "information",
      "log_messages": [
        "Mensagem 1",
        "Mensagem 2"
      ]
    }
  }

Campos
------

* *event*:

  * *type*: o tipo do evento. Deve ser um dos seguintes: *inventory_entry*, *pick_list_confirmation*, *pick_list_confirmation_log*, *pick_list_cancellation*, *pick_list_cancellation_log*, *sale_confirmation*, *sale_confirmation_log*, *inventory_adjustment*, *inventory_synchronization*, *inventory_return* ou *inventory_return_log*.
  * *occurred_at*: data e hora em que ocorreu o evento no ERP, formato ISO 8601.
  * *distribution_center_id*: o id do centro de distribuição. É obrigatório nos eventos *entrada de estoque*, *ajuste de estoque* e *sincronização de estoque*.
  * *pick_list_id*: o id da pick list associada a um evento. É obrigatório nos eventos *confirmação de pick list*, *log em confirmação de pick list*, *cancelamento de pick list* e *log em cancelamento de pick list*.
  * *transport_nfe_danfe_url*: a URL do DANFE da NFe de transporte. Pode ser informada no evento *confirmação de pick list*.
  * *transport_nfe_xml_url*: a URL do XML da NFe de transporte. Pode ser informada no evento *confirmação de pick list*.
  * *sale_id*: o id da venda. Deve ser informado nos eventos *confirmação de venda* e *log em confirmação de venda*.
  * *nfe_key*: a chave da NFe de venda. Pode ser informada no evento *confirmação de venda*.
  * *nfe_danfe_url*: a URL do DANFE da NFe de venda. Pode ser informada no evento *confirmação de venda*.
  * *nfe_xml_url*: a URL do XML da NFe de venda. Pode ser informada no evento *confirmação de venda*.
  * *machine_inventory_removal_id*: o id da baixa de estoque. Deve ser informado nos eventos *retorno de estoque* e *log de retorno de estoque*.
  * *log_level*: o nível de log. Pode ser um dentre os seguintes valores: *information*, *warning*, *error* ou *fatal*. A explicação de cada valor: *information* é usado para qualquer notificação informativa; *warning*, em caso de erro recuperável automaticamente pelo sistema; *error*, em caso de erro recuperável com interação do usuário; *fatal*, quando for um erro não recuperável. Este campo deve ser informado nos eventos *log em confirmação de pick list*, *log em cancelamento de pick list*, *log em confirmação de venda* e *log de retorno de estoque*.
  * *log_messages*: um array com as mensagens de log. Deve ser informado nos eventos *log em confirmação de pick list*, *log em cancelamento de pick list*, *log em confirmação de venda* e *log de retorno de estoque*.
  * *inventories*: array com os estoques a serem atualizados, um elemento por *storable* (produto). É obrigatório nos eventos *entrada de estoque*, *confirmação de pick list*, *cancelamento de pick list*, *ajuste de estoque*, *sincronização de estoque* e *retorno de estoque*. Pode ter no máximo 1000 itens nos eventos *entrada de estoque*, *ajuste de estoque* e *sincronização de estoque*; é ilimitado nos eventos *confirmação de pick list*, *cancelamento de pick list* e *retorno de estoque*.

    * *storable_id*: o id do produto.
    * *delta*: a diferença de estoque movimentada, positiva para entradas, negativas para saídas. Não é necessário informar na *sicronização de estoque*.
    * *balance*: o saldo final do estoque depois da movimentação.

Retorno
-------

======  ==============================
status  descrição
======  ==============================
200     Evento enfileirado com sucesso
======  ==============================

Erros
-----

======  =====================================  ===========================================
status  descrição                              response body
======  =====================================  ===========================================
400     parâmetros faltando                    { "status": "400", "error": "Bad Request" }
404     centro de distribuição não encontrado  { "status": "404", "error": "Not found" }
422     erro ao enfileirar evento              ver exemplo abaixo
======  =====================================  ===========================================

422 - erro ao enfileirar evento

::

  {
    "pick_list_id": [
      "não está aguardando confirmação"
    ]
  }

.. _services-erp:

Serviços implementados no ERP
*****************************

Estes são os serviços que devem ser implementados no ERP e que serão chamados pelo VMpay. Espera-se que estes serviços também sejam implementados de forma assíncrona.

Autenticação
============

A autenticação deverá ser realizada através de uma chave de API única gerada pelo sistema e atribuída a um usuário. O header *X-API-Key* deverá ser informado em todos os requests, pois o acesso à API só deverá ser permitido para usuários autenticados.

O valor do header deve ser algo como:

::

  X-API-Key: sua-chave-api

Caso uma chave de API não seja informada, o request deverá falhar com status 401. Caso uma chave de API não autorizada seja informada o request deverá falhar com o status 403.

Tipo do Conteúdo
================

As mensagens recebidas e enviadas pela API são em formato JSON. O header *Content-Type* deverá ser informado em todos os requests que enviem dados em formato JSON para o servidor.

O valor do header deve ser::

  Content-Type: application/json

Caso o tipo de conteúdo não seja informado corretamente, o request deverá falhar com status 415.

.. _service-erp-copl:

Confirmar pick list
===================

::

  POST /pick_lists

Request::

  {
    "pick_list": {
      "id": 12345,
      "machine_id": 12,
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "inventories": [
        {
          "storable_id": 123,
          "balance": 5
        },
        {
          "storable_id": 321,
          "balance": 10
        }
      ]
    }
  }

Campos
------

* *pick_list*:

  * *id*: o id da pick list.
  * *machine_id*: o id da máquina.
  * *occurred_at*: data e hora em que ocorreu a liberação da pick list no VMpay, formato ISO 8601.
  * *inventories*: array com os saldos da pick list, um elemento por *storable* (produto).

    * *storable_id*: o id do produto.
    * *balance*: o saldo do produto na pick list.

Retorno
-------

======  =========
status  descrição
======  =========
201     OK
======  =========

Erros
-----

======  ==================  ==================
status  descrição           response body
======  ==================  ==================
422     erros de validação  ver exemplo abaixo
======  ==================  ==================

422 - erros de validação

::

  {
    "errors": [
      "Produto 123 não encontrado",
      "Algum outro erro"
    ]
  }

.. _service-erp-capl:

Cancelar pick list
==================

::

  DELETE /pick_lists/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da pick list  sim
=========  ===============  ===========

Retorno
-------

======  =========  =============
status  descrição  response body
======  =========  =============
204     OK         (vazio)
======  =========  =============

Erros
-----

======  ========================  =========================================
status  descrição                 response body
======  ========================  =========================================
404     pick list não encontrada  { "status": "404", "error": "Not Found" }
======  ========================  =========================================

.. _service-erp-apl:

Aplicar pick list
=================

::

  POST /pick_lists/[id]/applyings

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id da pick list  sim
=========  ===============  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

.. _service-erp-rv:

Registrar venda
===============

::

  POST /sales

Request::

  {
    "sale": {
      "id": 120934,
      "machine_id": 12,
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "payment_method": {
        "id": 2,
        "description": "Cartão de crédito"
      },
      "cnpj_authorizer": "01027058000191",
      "authorization_code": "12345678",
      "card_brand": {
        "code": "01",
        "description": "Visa"
      },
      "consumer_cpf": "30851852912",
      "consumer_email": "user@vmpay.com.br",
      "total_price": 27.5,
      "total_quantity": 3.0,
      "items": [
        {
          "number": 1,
          "storable_id": 123,
          "unit_price": 5.0,
          "quantity": 1.0,
          "total_discount": 0,
          "total_price": 5.0
          "balance_after": 4.0
        },
        {
          "number": 2,
          "storable_id": 321,
          "unit_price": 12.0,
          "quantity": 2.0,
          "total_discount": 1.5,
          "total_price": 22.5,
          "balance_after": 8.0
        }
      ]
    }
  }

Campos
------

* *sale*:

  * *id*: o id da venda.
  * *machine_id*: o id da máquina onde ocorreu a venda.
  * *occurred_at*: data e hora em que ocorreu a venda no VMpay, formato ISO 8601.
  * *payment_method*: a forma de pagamento.

    * *id*: o id da forma de pagamento (tabela listada `abaixo <#payment-methods>`_).
    * *description*: a descrição da forma de pagamento

  * *cnpj_authorizer*: o CNPJ da credenciadora TEF.
  * *authorization_code*: o código de autorização TEF.
  * *card_brand*: a bandeira do cartão.

    * *code*: o código da bandeira. É um dentre os definidos pelo SEFAZ. A lista dos códigos disponíveis encontra-se `aqui <http://www.nfe.fazenda.gov.br/portal/exibirArquivo.aspx?conteudo=HoyGo5PttVk=>`_.
    * *description*: a descrição da bandeira.

  * *consumer_cpf*: CPF do consumidor (opcional).
  * *consumer_email*: e-mail do consumidor (opcional).
  * *total_price*: O preço total da venda.
  * *total_quantity*: A quantidade total da venda.
  * *items*: array com os itens da venda.

    * *number*: o número do item.
    * *storable_id*: o id do produto.
    * *unit_price*: o preço unitário do item.
    * *quantity*: a quantidade vendida do item.
    * *total_discount*: o desconto total do item.
    * *total_price*: o preço total do item.
    * *balance_after*: o saldo do produto na máquina após a venda.

.. _payment-methods:

Formas de Pagamento
-------------------

== ===================
id description
== ===================
1  Dinheiro
2  Cartão de crédito
3  Cartão de débito
4  Voucher alimentação
5  Voucher refeição
6  Private label
7  Créditos pré-pagos
8  PIX
9  PicPay
10 Mercado Pago
11 Ame Digital
12 Gran Coffee Digital
13 Crédito remoto
14 Autorizador externo
15 Indefinido
== ===================

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criada com sucesso
======  ==================

.. _service-erp-aem:

Ajustar estoques de máquina
===========================

::

  POST /machines/[id]/inventory_adjustments

Parâmetros de URL:
------------------

=========  =============  ===========
parâmetro  descrição      obrigatório
=========  =============  ===========
id         id da máquina  sim
=========  =============  ===========

Request::

  {
    "inventory_adjustment": {
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "inventories": [
        {
          "storable_id": 123,
          "delta": 1,
          "balance": 5
        },
        {
          "storable_id": 321,
          "delta": -1,
          "balance": 7
        }
      ]
    }
  }

Campos
------

* *inventory_adjustment*:

  * *occurred_at*: data e hora em que ocorreu o ajuste no VMpay, formato ISO 8601.
  * *inventories*: array com os estoques a serem ajustados, um elemento por *storable* (produto).

    * *storable_id*: o id do produto.
    * *delta*: a diferença de estoque.
    * *balance*: o saldo final do estoque depois do ajuste.

Retorno
-------

======  ==============================
status  descrição
======  ==============================
200     Atualização criada com sucesso
======  ==============================

.. _service-erp-bem:

Baixa de estoque de máquina
===========================

::

  POST /machines/[id]/inventory_removals

Parâmetros de URL:
------------------

=========  =============  ===========
parâmetro  descrição      obrigatório
=========  =============  ===========
id         id da máquina  sim
=========  =============  ===========

Request::

  {
    "inventory_removal": {
      "id": 8246,
      "distribution_center_id": 123,
      "occurred_at": "2022-05-25T12:34:56.000Z",
      "inventories": [
        {
          "storable_id": 123,
          "balance_before": 5
        },
        {
          "storable_id": 321,
          "balance_before": 6
        }
      ]
    }
  }

Campos
------

* *inventory_removal*:

  * *id*: o id da baixa de estoque.
  * *distribution_center_id*: o id do centro de distribuição de destino.
  * *occurred_at*: data e hora em que ocorreu a baixa de estoque no VMpay, formato ISO 8601.
  * *inventories*: array com os estoques a serem baixados, um elemento por *storable* (produto).

    * *storable_id*: o id do produto.
    * *balance_before*: o saldo do estoque logo *antes* da baixa.

Retorno
-------

======  ==============================
status  descrição
======  ==============================
200     Atualização criada com sucesso
======  ==============================
