##########
Auditorias
##########

Listar
======

Lista as auditorias de determinada máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/audits

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
      "id": 725818,
      "began_at": "2016-04-25T15:00:30.000-03:00",
      "ended_at": "2016-04-25T15:00:33.000-03:00",
      "total_quantity": 1,
      "total_value": 2.5
    },
    {
      "id": 725186,
      "began_at": "2016-04-25T11:50:27.000-03:00",
      "ended_at": "2016-04-25T11:50:31.000-03:00",
      "total_quantity": 7,
      "total_value": 19.85
    },
    {
      "id": 724622,
      "began_at": "2016-04-25T09:00:30.000-03:00",
      "ended_at": "2016-04-25T09:00:33.000-03:00",
      "total_quantity": 1,
      "total_value": 3
    }
  ]

Ver
===

Mostra determinada auditoria de uma máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/audits/[id]

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id da auditoria   sim
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
    "id": 725186,
    "occurred_at": "2016-04-25T11:50:27.000-03:00",
    "total_vends_value": 55,
    "total_vends_quantity": 500,
    "planogram_items": [
      {
        "locator": "10",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "11",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "12",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "13",
        "total_vends_value": 0.1,
        "total_vends_quantity": 0
      },
      {
        "locator": "14",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "15",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "16",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "17",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "18",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "19",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "20",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "21",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "22",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "23",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "24",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "25",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "26",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "27",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "28",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "29",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "30",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "31",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "32",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "33",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "34",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "35",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "36",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "37",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "38",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "39",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "40",
        "total_vends_value": 7.8,
        "total_vends_quantity": 59
      },
      {
        "locator": "41",
        "total_vends_value": 6.8,
        "total_vends_quantity": 68
      },
      {
        "locator": "42",
        "total_vends_value": 6.5,
        "total_vends_quantity": 65
      },
      {
        "locator": "43",
        "total_vends_value": 5.9,
        "total_vends_quantity": 58
      },
      {
        "locator": "44",
        "total_vends_value": 7,
        "total_vends_quantity": 70
      },
      {
        "locator": "45",
        "total_vends_value": 7.6,
        "total_vends_quantity": 76
      },
      {
        "locator": "46",
        "total_vends_value": 5.3,
        "total_vends_quantity": 51
      },
      {
        "locator": "47",
        "total_vends_value": 6.5,
        "total_vends_quantity": 38
      },
      {
        "locator": "48",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "49",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "50",
        "total_vends_value": 0.1,
        "total_vends_quantity": 1
      },
      {
        "locator": "51",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "52",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "53",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "54",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "55",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "56",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "57",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "58",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "59",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "60",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "61",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "62",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "63",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "64",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "65",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "66",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "67",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "68",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "69",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "70",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "71",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "72",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "73",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "74",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "75",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "76",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "77",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "78",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "79",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "80",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "81",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "82",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "83",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "84",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "85",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "86",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "87",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "88",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "89",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "90",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "91",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "92",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "93",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "94",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      }
    ]
  }

Erros
-----

======  ===========================================  =========================================
status  descrição                                    response body
======  ===========================================  =========================================
404     máquina/instalação/auditoria não encontrada  { "status": "404", "error": "Not Found" }
======  ===========================================  =========================================


Baixar em formato TXT
=====================

Baixa determinada auditoria de uma máquina e instalação em formato TXT.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/audits/[id].txt

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id da auditoria   sim
===============  ================  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  DXS*NBF1234567*VA*V0/6*1
  ST*001*0001
  CA1*0
  CA2*2878109*125903*2878109*60367
  CA3*3227279*1536695*6777215*1690584**1536695*10545640*1690584
  CA4*10872370*105695*10872370*105695
  CA7*0*0
  CA8*21415*21415
  CA9*321365*321365
  CA10*0*0
  CA11*0*6340*2935*3405*6340*2935*3405
  CA11*0*1474*1474*0*1474*1474*0
  CA11*0*12912*7928*4984*12912*7928*4984
  CA11*0*3142*3142*0*3142*3142*0
  CA11*0*23988*5681*18307*23988*5681*18307
  CA11*0*3108*3108*0*3108*3108*0
  CA11*0*35375*7412*27963*35375*7412*27963
  CA11*0*6507*3832*2675*6507*3832*2675
  CA11*0*18050*4180*13870*83586*4180*79406
  CA11*0*6329*843*5486*6329*843*5486
  CA11*0*1282*1282*0*1282*1282*0
  CA11*0*83*83*0*83*83*0
  CA11*0*10*10*0*10*10*0
  CA11*0*0*0*0*0*0*0
  CA11*0*0*0*0*0*0*0
  CA11*0*0*0*0*0*0*0
  CA14*0*13632**13632
  CA14*0*36902**36902
  CA14*0*13552**13552
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA14*0*0**0
  CA15*
  CA15*
  DA1*000000000000000*000000000000*0000
  DA2*0*0*0*0
  DA4*0*0
  DA5*0**0
  EA1*EBB*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EAR*000000*000000
  EA1*EC1C*000000*000000
  EA1*EBB*000000*000000
  EA1*EAR*000000*000000
  EA1*EBB*000000*000000
  EA1*EBB*000000*000000
  EA2*ECM*0*0*0
  EA2*EAR*72*72*0
  EA2*ECF*1*1*0
  EA2*ECE*2*2*0
  EA2*EAJ*0*0*0
  EA2*EC1C*12*12*0
  EA2*EC1C_2*0*0*0
  EA2*EDP*8*8*0
  EA2*EBB*96*96*1
  EA2*EDF_1*0*0*0
  EA2*ECA*0*0*0
  EA2*ECK*1*1*0
  EA2*EGN*68*68*0
  EA2*EBI*21*21*0
  EA2*ELA*1*1*0
  EA2*EDF_2*22*22*0
  EA2*EEJ*71*71*1
  EA2*EDJ_P*5*5*0
  EA2*EDJ_GR*0*0*0
  EA2*EBJ*0*0*0
  EA2*EFB*63*63*0
  EA2*EDO_1*66*66*0
  EA2*OAR*61*61*0
  EA2*EFI*66*66*0
  EA2*EEL*6*6*0
  EA2*EDO_2*6*6*0
  EA2*EDZ*6*6*0
  EA2*EEC_ES1*6*6*0
  EA2*EEC_FB1*0*0*0
  EA2*EEC_FB2*0*0*0
  EA2*EDM_1*1*1*0
  EA2*EDM_2*2*2*0
  EA2*EH1A*0*0*0
  EA2*EFE*0*0*0
  EA2*ELE_P*0*0*0
  EA2*ELE_GR*0*0*0
  EA2*EBL*0*0*0
  EA2*EFN_1*2*2*0
  EA2*EEK*8*8*0
  EA2*EDT_1*19*19*0
  EA2*EDU_1*2*2*0
  EA2*EDT_2*0*0*0
  EA2*EDU_2*0*0*0
  EA2*EFN_2*2*2*0
  EA2*ELC*0*0*0
  EA2*ECE_A*0*0*0
  EA2*ECE_B*0*0*0
  EA2*ECA_A*0*0*0
  EA2*ECA_B*0*0*0
  EA2*EJM_A*0*0*0
  EA2*EJM_B*0*0*0
  EA2*EJL_A*0*0*0
  EA2*EJL_B*0*0*0
  EA2*EJJ_A*2*2*0
  EA2*EJJ_B*0*0*0
  EA2*EJK_A*0*0*0
  EA2*EJK_B*0*0*0
  EA2*ECQ*1*257*0
  EA2*EJB_A*74*74*0
  EA2*EAREC*0*0*0
  EA3*0*000000*0000**000000*0000
  EA6*000000*0000
  EA7*9491*9491
  ID1*0*930E*4*0*MDB *0000000000
  ID4*2*39
  ID5*000000*0000
  ID7*
  ID7*1**000*000000000000*000000000000*0000
  PA1*01*10
  PA2*5487**5487
  PA3*211**211
  PA4*0**0
  PA6******0
  PA7*01*CA*0*10*0*0*0*0
  PA7*01*DA*0*10*0*0*0*0
  PA7*01*DA*1*65535*0*0*0*0
  PA7*01*DA*2*65535*0*0*0*0
  PA7*01*DB*0*10*0*0*0*0
  PA7*01*DB*1*65535*0*0*0*0
  PA7*01*DB*2*65535*0*0*0*0
  PA1*02*10
  PA2*13773**13773
  PA3*267**267
  PA4*0**0
  PA6******0
  PA7*02*CA*0*10*0*0*0*0
  PA7*02*DA*0*10*0*0*0*0
  PA7*02*DA*1*65535*0*0*0*0
  PA7*02*DA*2*65535*0*0*0*0
  PA7*02*DB*0*10*0*0*0*0
  PA7*02*DB*1*65535*0*0*0*0
  PA7*02*DB*2*65535*0*0*0*0
  PA1*03*10
  PA2*1299**1299
  PA3*24**24
  PA4*0**0
  PA6******0
  PA7*03*CA*0*10*0*0*0*0
  PA7*03*DA*0*10*0*0*0*0
  PA7*03*DA*1*65535*0*0*0*0
  PA7*03*DA*2*65535*0*0*0*0
  PA7*03*DB*0*10*0*0*0*0
  PA7*03*DB*1*65535*0*0*0*0
  PA7*03*DB*2*65535*0*0*0*0
  PA1*04*10
  PA2*10405**10405
  PA3*518**518
  PA4*0**0
  PA6******0
  PA7*04*CA*0*10*0*0*0*0
  PA7*04*DA*0*10*0*0*0*0
  PA7*04*DA*1*65535*0*0*0*0
  PA7*04*DA*2*65535*0*0*0*0
  PA7*04*DB*0*10*0*0*0*0
  PA7*04*DB*1*65535*0*0*0*0
  PA7*04*DB*2*65535*0*0*0*0
  PA1*05*10
  PA2*3549**3549
  PA3*132**132
  PA4*94**94
  PA6******0
  PA7*05*CA*0*10*0*0*0*0
  PA7*05*DA*0*10*0*0*0*0
  PA7*05*DA*1*65535*0*0*0*0
  PA7*05*DA*2*65535*0*0*0*0
  PA7*05*DB*0*10*0*0*0*0
  PA7*05*DB*1*65535*0*0*0*0
  PA7*05*DB*2*65535*0*0*0*0
  PA1*06*10
  PA2*8031**8031
  PA3*307**307
  PA4*30**30
  PA6******0
  PA7*06*CA*0*10*0*0*0*0
  PA7*06*DA*0*10*0*0*0*0
  PA7*06*DA*1*65535*0*0*0*0
  PA7*06*DA*2*65535*0*0*0*0
  PA7*06*DB*0*10*0*0*0*0
  PA7*06*DB*1*65535*0*0*0*0
  PA7*06*DB*2*65535*0*0*0*0
  PA1*07*10
  PA2*3380**3380
  PA3*210**210
  PA4*48**48
  PA6******0
  PA7*07*CA*0*10*0*0*0*0
  PA7*07*DA*0*10*0*0*0*0
  PA7*07*DA*1*65535*0*0*0*0
  PA7*07*DA*2*65535*0*0*0*0
  PA7*07*DB*0*10*0*0*0*0
  PA7*07*DB*1*65535*0*0*0*0
  PA7*07*DB*2*65535*0*0*0*0
  PA1*08*10
  PA2*8787**8787
  PA3*212**212
  PA4*58**58
  PA6******0
  PA7*08*CA*0*10*0*0*0*0
  PA7*08*DA*0*10*0*0*0*0
  PA7*08*DA*1*65535*0*0*0*0
  PA7*08*DA*2*65535*0*0*0*0
  PA7*08*DB*0*10*0*0*0*0
  PA7*08*DB*1*65535*0*0*0*0
  PA7*08*DB*2*65535*0*0*0*0
  PA1*09*10
  PA2*2430**2430
  PA3*27**27
  PA4*34**34
  PA6******0
  PA7*09*CA*0*10*0*0*0*0
  PA7*09*DA*0*10*0*0*0*0
  PA7*09*DA*1*65535*0*0*0*0
  PA7*09*DA*2*65535*0*0*0*0
  PA7*09*DB*0*10*0*0*0*0
  PA7*09*DB*1*65535*0*0*0*0
  PA7*09*DB*2*65535*0*0*0*0
  PA1*10*10
  PA2*2668**2668
  PA3*67**67
  PA4*316**316
  PA6******0
  PA7*10*CA*0*10*0*0*0*0
  PA7*10*DA*0*10*0*0*0*0
  PA7*10*DA*1*65535*0*0*0*0
  PA7*10*DA*2*65535*0*0*0*0
  PA7*10*DB*0*10*0*0*0*0
  PA7*10*DB*1*65535*0*0*0*0
  PA7*10*DB*2*65535*0*0*0*0
  PA1*11*10
  PA2*2987**2987
  PA3*62**62
  PA4*79**79
  PA6******0
  PA7*11*CA*0*10*0*0*0*0
  PA7*11*DA*0*10*0*0*0*0
  PA7*11*DA*1*65535*0*0*0*0
  PA7*11*DA*2*65535*0*0*0*0
  PA7*11*DB*0*10*0*0*0*0
  PA7*11*DB*1*65535*0*0*0*0
  PA7*11*DB*2*65535*0*0*0*0
  PA1*12*10
  PA2*7352**7352
  PA3*1377**1377
  PA4*105**105
  PA6******0
  PA7*12*CA*0*10*0*0*0*0
  PA7*12*DA*0*10*0*0*0*0
  PA7*12*DA*1*65535*0*0*0*0
  PA7*12*DA*2*65535*0*0*0*0
  PA7*12*DB*0*10*0*0*0*0
  PA7*12*DB*1*65535*0*0*0*0
  PA7*12*DB*2*65535*0*0*0*0
  PA1*13*10
  PA2*145**145
  PA3*8**8
  PA4*77**77
  PA6******0
  PA7*13*CA*0*10*0*0*0*0
  PA7*13*DA*0*10*0*0*0*0
  PA7*13*DA*1*65535*0*0*0*0
  PA7*13*DA*2*65535*0*0*0*0
  PA7*13*DB*0*10*0*0*0*0
  PA7*13*DB*1*65535*0*0*0*0
  PA7*13*DB*2*65535*0*0*0*0
  PA1*14*10
  PA2*845**845
  PA3*6**6
  PA4*353**353
  PA6******0
  PA7*14*CA*0*10*0*0*0*0
  PA7*14*DA*0*10*0*0*0*0
  PA7*14*DA*1*65535*0*0*0*0
  PA7*14*DA*2*65535*0*0*0*0
  PA7*14*DB*0*10*0*0*0*0
  PA7*14*DB*1*65535*0*0*0*0
  PA7*14*DB*2*65535*0*0*0*0
  PA1*15*10
  PA2*651**651
  PA3*16**16
  PA4*7**7
  PA6******0
  PA7*15*CA*0*10*0*0*0*0
  PA7*15*DA*0*10*0*0*0*0
  PA7*15*DA*1*65535*0*0*0*0
  PA7*15*DA*2*65535*0*0*0*0
  PA7*15*DB*0*10*0*0*0*0
  PA7*15*DB*1*65535*0*0*0*0
  PA7*15*DB*2*65535*0*0*0*0
  PA1*16*10
  PA2*5947**5947
  PA3*105**105
  PA4*0**0
  PA6******0
  PA7*16*CA*0*10*0*0*0*0
  PA7*16*DA*0*10*0*0*0*0
  PA7*16*DA*1*65535*0*0*0*0
  PA7*16*DA*2*65535*0*0*0*0
  PA7*16*DB*0*10*0*0*0*0
  PA7*16*DB*1*65535*0*0*0*0
  PA7*16*DB*2*65535*0*0*0*0
  PA1*17*10
  PA2*2**2
  PA3*2**2
  PA4*2**2
  PA6******0
  PA7*17*CA*0*10*0*0*0*0
  PA7*17*DA*0*10*0*0*0*0
  PA7*17*DA*1*65535*0*0*0*0
  PA7*17*DA*2*65535*0*0*0*0
  PA7*17*DB*0*10*0*0*0*0
  PA7*17*DB*1*65535*0*0*0*0
  PA7*17*DB*2*65535*0*0*0*0
  PA1*18*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*18*CA*0*10*0*0*0*0
  PA7*18*DA*0*10*0*0*0*0
  PA7*18*DA*1*65535*0*0*0*0
  PA7*18*DA*2*65535*0*0*0*0
  PA7*18*DB*0*10*0*0*0*0
  PA7*18*DB*1*65535*0*0*0*0
  PA7*18*DB*2*65535*0*0*0*0
  PA1*19*10
  PA2*5**5
  PA3*0**0
  PA4*5**5
  PA6******0
  PA7*19*CA*0*10*0*0*0*0
  PA7*19*DA*0*10*0*0*0*0
  PA7*19*DA*1*65535*0*0*0*0
  PA7*19*DA*2*65535*0*0*0*0
  PA7*19*DB*0*10*0*0*0*0
  PA7*19*DB*1*65535*0*0*0*0
  PA7*19*DB*2*65535*0*0*0*0
  PA1*20*10
  PA2*33**33
  PA3*0**0
  PA4*33**33
  PA6******0
  PA7*20*CA*0*10*0*0*0*0
  PA7*20*DA*0*10*0*0*0*0
  PA7*20*DA*1*65535*0*0*0*0
  PA7*20*DA*2*65535*0*0*0*0
  PA7*20*DB*0*10*0*0*0*0
  PA7*20*DB*1*65535*0*0*0*0
  PA7*20*DB*2*65535*0*0*0*0
  PA1*21*10
  PA2*27**27
  PA3*1**1
  PA4*1**1
  PA6******0
  PA7*21*CA*0*10*0*0*0*0
  PA7*21*DA*0*10*0*0*0*0
  PA7*21*DA*1*65535*0*0*0*0
  PA7*21*DA*2*65535*0*0*0*0
  PA7*21*DB*0*10*0*0*0*0
  PA7*21*DB*1*65535*0*0*0*0
  PA7*21*DB*2*65535*0*0*0*0
  PA1*22*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*22*CA*0*10*0*0*0*0
  PA7*22*DA*0*10*0*0*0*0
  PA7*22*DA*1*65535*0*0*0*0
  PA7*22*DA*2*65535*0*0*0*0
  PA7*22*DB*0*10*0*0*0*0
  PA7*22*DB*1*65535*0*0*0*0
  PA7*22*DB*2*65535*0*0*0*0
  PA1*23*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*23*CA*0*10*0*0*0*0
  PA7*23*DA*0*10*0*0*0*0
  PA7*23*DA*1*65535*0*0*0*0
  PA7*23*DA*2*65535*0*0*0*0
  PA7*23*DB*0*10*0*0*0*0
  PA7*23*DB*1*65535*0*0*0*0
  PA7*23*DB*2*65535*0*0*0*0
  PA1*24*10
  PA2*2**2
  PA3*0**0
  PA4*2**2
  PA6******0
  PA7*24*CA*0*10*0*0*0*0
  PA7*24*DA*0*10*0*0*0*0
  PA7*24*DA*1*65535*0*0*0*0
  PA7*24*DA*2*65535*0*0*0*0
  PA7*24*DB*0*10*0*0*0*0
  PA7*24*DB*1*65535*0*0*0*0
  PA7*24*DB*2*65535*0*0*0*0
  PA1*25*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*25*CA*0*10*0*0*0*0
  PA7*25*DA*0*10*0*0*0*0
  PA7*25*DA*1*65535*0*0*0*0
  PA7*25*DA*2*65535*0*0*0*0
  PA7*25*DB*0*10*0*0*0*0
  PA7*25*DB*1*65535*0*0*0*0
  PA7*25*DB*2*65535*0*0*0*0
  PA1*26*10
  PA2*1**1
  PA3*0**0
  PA4*1**1
  PA6******0
  PA7*26*CA*0*10*0*0*0*0
  PA7*26*DA*0*10*0*0*0*0
  PA7*26*DA*1*65535*0*0*0*0
  PA7*26*DA*2*65535*0*0*0*0
  PA7*26*DB*0*10*0*0*0*0
  PA7*26*DB*1*65535*0*0*0*0
  PA7*26*DB*2*65535*0*0*0*0
  PA1*27*10
  PA2*32**32
  PA3*2**2
  PA4*0**0
  PA6******0
  PA7*27*CA*0*10*0*0*0*0
  PA7*27*DA*0*10*0*0*0*0
  PA7*27*DA*1*65535*0*0*0*0
  PA7*27*DA*2*65535*0*0*0*0
  PA7*27*DB*0*10*0*0*0*0
  PA7*27*DB*1*65535*0*0*0*0
  PA7*27*DB*2*65535*0*0*0*0
  PA1*28*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*28*CA*0*10*0*0*0*0
  PA7*28*DA*0*10*0*0*0*0
  PA7*28*DA*1*65535*0*0*0*0
  PA7*28*DA*2*65535*0*0*0*0
  PA7*28*DB*0*10*0*0*0*0
  PA7*28*DB*1*65535*0*0*0*0
  PA7*28*DB*2*65535*0*0*0*0
  PA1*29*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*29*CA*0*10*0*0*0*0
  PA7*29*DA*0*10*0*0*0*0
  PA7*29*DA*1*65535*0*0*0*0
  PA7*29*DA*2*65535*0*0*0*0
  PA7*29*DB*0*10*0*0*0*0
  PA7*29*DB*1*65535*0*0*0*0
  PA7*29*DB*2*65535*0*0*0*0
  PA1*30*10
  PA2*0**0
  PA3*0**0
  PA4*0**0
  PA6******0
  PA7*30*CA*0*10*0*0*0*0
  PA7*30*DA*0*10*0*0*0*0
  PA7*30*DA*1*65535*0*0*0*0
  PA7*30*DA*2*65535*0*0*0*0
  PA7*30*DB*0*10*0*0*0*0
  PA7*30*DB*1*65535*0*0*0*0
  PA7*30*DB*2*65535*0*0*0*0
  PA11*0
  PA1*V33*10
  PA2*3291**3291
  PA3*62**62
  PA4*1**1
  SA1*V33*0****000000000000
  PA7*V33*CA*0*10*0*0*0*0
  PA7*V33*DA*0*10*0*0*0*0
  PA7*V33*DA*1*65535*0*0*0*0
  PA7*V33*DA*2*65535*0*0*0*0
  PA7*V33*DB*0*10*0*0*0*0
  PA7*V33*DB*1*65535*0*0*0*0
  PA7*V33*DB*2*65535*0*0*0*0
  PA1*V35*10
  PA2*1727**1727
  PA3*15**15
  PA4*1**1
  SA1*V35*0****000000000000
  PA7*V35*CA*0*10*0*0*0*0
  PA7*V35*DA*0*10*0*0*0*0
  PA7*V35*DA*1*65535*0*0*0*0
  PA7*V35*DA*2*65535*0*0*0*0
  PA7*V35*DB*0*10*0*0*0*0
  PA7*V35*DB*1*65535*0*0*0*0
  PA7*V35*DB*2*65535*0*0*0*0
  PA1*V36*10
  PA2*3452**3452
  PA3*39**39
  PA4*0**0
  SA1*V36*0****000000000000
  PA7*V36*CA*0*10*0*0*0*0
  PA7*V36*DA*0*10*0*0*0*0
  PA7*V36*DA*1*65535*0*0*0*0
  PA7*V36*DA*2*65535*0*0*0*0
  PA7*V36*DB*0*10*0*0*0*0
  PA7*V36*DB*1*65535*0*0*0*0
  PA7*V36*DB*2*65535*0*0*0*0
  PA1*V38*10
  PA2*1776**1776
  PA3*20**20
  PA4*0**0
  SA1*V38*0****000000000000
  PA7*V38*CA*0*10*0*0*0*0
  PA7*V38*DA*0*10*0*0*0*0
  PA7*V38*DA*1*65535*0*0*0*0
  PA7*V38*DA*2*65535*0*0*0*0
  PA7*V38*DB*0*10*0*0*0*0
  PA7*V38*DB*1*65535*0*0*0*0
  PA7*V38*DB*2*65535*0*0*0*0
  PA1*V43*10
  PA2*1505**1505
  PA3*7**7
  PA4*0**0
  SA1*V43*0****000000000000
  PA7*V43*CA*0*10*0*0*0*0
  PA7*V43*DA*0*10*0*0*0*0
  PA7*V43*DA*1*65535*0*0*0*0
  PA7*V43*DA*2*65535*0*0*0*0
  PA7*V43*DB*0*10*0*0*0*0
  PA7*V43*DB*1*65535*0*0*0*0
  PA7*V43*DB*2*65535*0*0*0*0
  PA1*V45*10
  PA2*1756**1756
  PA3*13**13
  PA4*1**1
  SA1*V45*0****000000000000
  PA7*V45*CA*0*10*0*0*0*0
  PA7*V45*DA*0*10*0*0*0*0
  PA7*V45*DA*1*65535*0*0*0*0
  PA7*V45*DA*2*65535*0*0*0*0
  PA7*V45*DB*0*10*0*0*0*0
  PA7*V45*DB*1*65535*0*0*0*0
  PA7*V45*DB*2*65535*0*0*0*0
  PA1*V46*10
  PA2*1425**1425
  PA3*15**15
  PA4*0**0
  SA1*V46*0****000000000000
  PA7*V46*CA*0*10*0*0*0*0
  PA7*V46*DA*0*10*0*0*0*0
  PA7*V46*DA*1*65535*0*0*0*0
  PA7*V46*DA*2*65535*0*0*0*0
  PA7*V46*DB*0*10*0*0*0*0
  PA7*V46*DB*1*65535*0*0*0*0
  PA7*V46*DB*2*65535*0*0*0*0
  PA1*V47*10
  PA2*1427**1427
  PA3*16**16
  PA4*0**0
  SA1*V47*0****000000000000
  PA7*V47*CA*0*10*0*0*0*0
  PA7*V47*DA*0*10*0*0*0*0
  PA7*V47*DA*1*65535*0*0*0*0
  PA7*V47*DA*2*65535*0*0*0*0
  PA7*V47*DB*0*10*0*0*0*0
  PA7*V47*DB*1*65535*0*0*0*0
  PA7*V47*DB*2*65535*0*0*0*0
  PA1*V48*10
  PA2*1384**1384
  PA3*27**27
  PA4*0**0
  SA1*V48*0****000000000000
  PA7*V48*CA*0*10*0*0*0*0
  PA7*V48*DA*0*10*0*0*0*0
  PA7*V48*DA*1*65535*0*0*0*0
  PA7*V48*DA*2*65535*0*0*0*0
  PA7*V48*DB*0*10*0*0*0*0
  PA7*V48*DB*1*65535*0*0*0*0
  PA7*V48*DB*2*65535*0*0*0*0
  PA1*V51*10
  PA2*1235**1235
  PA3*43**43
  PA4*0**0
  SA1*V51*0****000000000000
  PA7*V51*CA*0*10*0*0*0*0
  PA7*V51*DA*0*10*0*0*0*0
  PA7*V51*DA*1*65535*0*0*0*0
  PA7*V51*DA*2*65535*0*0*0*0
  PA7*V51*DB*0*10*0*0*0*0
  PA7*V51*DB*1*65535*0*0*0*0
  PA7*V51*DB*2*65535*0*0*0*0
  PA1*V52*10
  PA2*1313**1313
  PA3*19**19
  PA4*0**0
  SA1*V52*0****000000000000
  PA7*V52*CA*0*10*0*0*0*0
  PA7*V52*DA*0*10*0*0*0*0
  PA7*V52*DA*1*65535*0*0*0*0
  PA7*V52*DA*2*65535*0*0*0*0
  PA7*V52*DB*0*10*0*0*0*0
  PA7*V52*DB*1*65535*0*0*0*0
  PA7*V52*DB*2*65535*0*0*0*0
  PA1*V53*10
  PA2*1199**1199
  PA3*16**16
  PA4*0**0
  SA1*V53*0****000000000000
  PA7*V53*CA*0*10*0*0*0*0
  PA7*V53*DA*0*10*0*0*0*0
  PA7*V53*DA*1*65535*0*0*0*0
  PA7*V53*DA*2*65535*0*0*0*0
  PA7*V53*DB*0*10*0*0*0*0
  PA7*V53*DB*1*65535*0*0*0*0
  PA7*V53*DB*2*65535*0*0*0*0
  PA1*V54*10
  PA2*1231**1231
  PA3*26**26
  PA4*0**0
  SA1*V54*0****000000000000
  PA7*V54*CA*0*10*0*0*0*0
  PA7*V54*DA*0*10*0*0*0*0
  PA7*V54*DA*1*65535*0*0*0*0
  PA7*V54*DA*2*65535*0*0*0*0
  PA7*V54*DB*0*10*0*0*0*0
  PA7*V54*DB*1*65535*0*0*0*0
  PA7*V54*DB*2*65535*0*0*0*0
  PA1*V55*10
  PA2*1346**1346
  PA3*16**16
  PA4*0**0
  SA1*V55*0****000000000000
  PA7*V55*CA*0*10*0*0*0*0
  PA7*V55*DA*0*10*0*0*0*0
  PA7*V55*DA*1*65535*0*0*0*0
  PA7*V55*DA*2*65535*0*0*0*0
  PA7*V55*DB*0*10*0*0*0*0
  PA7*V55*DB*1*65535*0*0*0*0
  PA7*V55*DB*2*65535*0*0*0*0
  PA1*V56*10
  PA2*1808**1808
  PA3*21**21
  PA4*0**0
  SA1*V56*0****000000000000
  PA7*V56*CA*0*10*0*0*0*0
  PA7*V56*DA*0*10*0*0*0*0
  PA7*V56*DA*1*65535*0*0*0*0
  PA7*V56*DA*2*65535*0*0*0*0
  PA7*V56*DB*0*10*0*0*0*0
  PA7*V56*DB*1*65535*0*0*0*0
  PA7*V56*DB*2*65535*0*0*0*0
  PA1*V57*10
  PA2*1739**1739
  PA3*16**16
  PA4*0**0
  SA1*V57*0****000000000000
  PA7*V57*CA*0*10*0*0*0*0
  PA7*V57*DA*0*10*0*0*0*0
  PA7*V57*DA*1*65535*0*0*0*0
  PA7*V57*DA*2*65535*0*0*0*0
  PA7*V57*DB*0*10*0*0*0*0
  PA7*V57*DB*1*65535*0*0*0*0
  PA7*V57*DB*2*65535*0*0*0*0
  PA1*V58*10
  PA2*1435**1435
  PA3*18**18
  PA4*0**0
  SA1*V58*0****000000000000
  PA7*V58*CA*0*10*0*0*0*0
  PA7*V58*DA*0*10*0*0*0*0
  PA7*V58*DA*1*65535*0*0*0*0
  PA7*V58*DA*2*65535*0*0*0*0
  PA7*V58*DB*0*10*0*0*0*0
  PA7*V58*DB*1*65535*0*0*0*0
  PA7*V58*DB*2*65535*0*0*0*0
  SA1*BOX 1*0****000000000000
  SA1*BOX 2*0****000000000000
  SA1*BOX 3*0****000000000000
  SA1*BOX 4*0****000000000000
  SA1*BOX 5*0****000000000000
  SA1*BOX 6*0****000000000000
  SA1*BOX 7*0****000000000000
  SA1*BOX 8*
  SA1*GRAINS*0*000000000000
  SA1*CUP*0*000000000000
  VA1*19653850*131315*2876634*131315
  VA2**4161**4161
  VA3**1261*0*1261
  G85*AEAC
  SE*710*0001
  DXE*1*1


Erros
-----

======  ===========================================  =========================================
status  descrição                                    response body
======  ===========================================  =========================================
404     máquina/instalação/auditoria não encontrada  { "status": "404", "error": "Not Found" }
======  ===========================================  =========================================




Ver última auditoria
====================

Mostra última auditoria de uma máquina e instalação.

::

  GET /api/v1/machines/[machine_id]/installations/[installation_id]/last_audit

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
    "id": 725186,
    "occurred_at": "2016-04-25T11:50:27.000-03:00",
    "total_vends_value": 55,
    "total_vends_quantity": 500,
    "planogram_items": [
      {
        "locator": "10",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "11",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "12",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "13",
        "total_vends_value": 0.1,
        "total_vends_quantity": 0
      },
      {
        "locator": "14",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "15",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "16",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "17",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "18",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "19",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "20",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "21",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "22",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "23",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "24",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "25",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "26",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "27",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "28",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "29",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "30",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "31",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "32",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "33",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "34",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "35",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "36",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "37",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "38",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "39",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "40",
        "total_vends_value": 7.8,
        "total_vends_quantity": 59
      },
      {
        "locator": "41",
        "total_vends_value": 6.8,
        "total_vends_quantity": 68
      },
      {
        "locator": "42",
        "total_vends_value": 6.5,
        "total_vends_quantity": 65
      },
      {
        "locator": "43",
        "total_vends_value": 5.9,
        "total_vends_quantity": 58
      },
      {
        "locator": "44",
        "total_vends_value": 7,
        "total_vends_quantity": 70
      },
      {
        "locator": "45",
        "total_vends_value": 7.6,
        "total_vends_quantity": 76
      },
      {
        "locator": "46",
        "total_vends_value": 5.3,
        "total_vends_quantity": 51
      },
      {
        "locator": "47",
        "total_vends_value": 6.5,
        "total_vends_quantity": 38
      },
      {
        "locator": "48",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "49",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "50",
        "total_vends_value": 0.1,
        "total_vends_quantity": 1
      },
      {
        "locator": "51",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "52",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "53",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "54",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "55",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "56",
        "total_vends_value": 0.2,
        "total_vends_quantity": 2
      },
      {
        "locator": "57",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "58",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "59",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "60",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "61",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "62",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "63",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "64",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "65",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "66",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "67",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "68",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "69",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "70",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "71",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "72",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "73",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "74",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "75",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "76",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "77",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "78",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "79",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "80",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "81",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "82",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "83",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "84",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "85",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "86",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "87",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "88",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "89",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "90",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "91",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "92",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "93",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      },
      {
        "locator": "94",
        "total_vends_value": 0,
        "total_vends_quantity": 0
      }
    ]
  }

Erros
-----

======  ===========================================  =========================================
status  descrição                                    response body
======  ===========================================  =========================================
404     máquina/instalação/auditoria não encontrada  { "status": "404", "error": "Not Found" }
======  ===========================================  =========================================

Desprocessar
============

Desprocessa auditoria. Pode ser utilizado em auditorias cujos valores vieram
errados. Desprocessa vendas, valores em dinheiro/moeda e coletas.

::

  DELETE /api/v1/machines/[machine_id]/installations/[installation_id]/audits/[id]

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
id               id da auditoria   sim
===============  ================  ===========

Retorno
-------

======  =========================  =============
status  descrição                  response body
======  =========================  =============
204     Desprocessada com sucesso  (vazio)
======  =========================  =============

Erros
-----

======  ===========================================  =========================================
status  descrição                                    response body
======  ===========================================  =========================================
404     máquina/instalação/auditoria não encontrada  { "status": "404", "error": "Not Found" }
======  ===========================================  =========================================
