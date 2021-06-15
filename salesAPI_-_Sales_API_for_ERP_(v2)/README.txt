This document contains the necessary data and requirements for integration with the __salesAPI conector__, a passive API to connect  __Sales systems (E-commerce B2C, B2B, CRM, POS and WMS systems)__ with ERP systems, as SAP Business One or TOTVS Protheus.

__salesAPI conector currently has the following HTTP REST Plain services - version 2 (v2.3):
- branches: search branches in ERP
- warehouses: search warehouses in ERP
- binLocations: search bin locations in ERP
- usages: search usages in ERP
- carriers: search carriers in ERP
- itemGroups: search product groups in ERP
- products: search products (with or without Partnumber) and prices in ERP
- stocks: search inventory in ERP
- pricelists: search pricelists in ERP
- prices: search prices in ERP
- partners: search and insert business partners in ERP
- contacts: search and insert partner contacts in ERP
- saleContracts: search sale contracts in ERP
- quotations: search and insert sale quotations in ERP
- orders: search and insert sale orders in ERP
- orderStatus: seach for changes in the status of sale orders in ERP (only SAP Business One)
- picklists: insert sale picklists in ERP
- invoices: search and insert sale invoices in ERP
- deliveries: search and insert sale deliveries in ERP (only SAP Business One)
- creditNotes: search sale credit notes in ERP
- downPayments: search sale down payments in ERP (only SAP Business One)
- receivables: search receivables in ERP
- incPayments: search incoming payments in ERP
 
***

__Content Type__: all salesAPI services use the “content-type” application/json for Parameters (body request) and Responses.

__Authentication__: salesAPI uses Basic Authentication (user/password)

__Characteristics__: pagination, incremental query, default fields, objects and processes, use of custom fields (limited use), API usage and ERP transactions monitoring