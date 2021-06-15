This document contains the data and requirements necessary for the integration with the __mesAPI conector__, a passive API to connect  __Shoop Floor and MES systems__ with ERP systems, as SAP Business One or TOTVS Protheus.

__mesAPI conector currently has the following HTTP REST Plain services - version 2 (v2.0.2):
- billOfMaterials: search bill of materials in ERP
- productionResources: search production resources in ERP
- resourceGroups: search work centers in ERP
- tools: search tools in ERP
- operators: search operators in ERP
- stopReasons: search stop reasons  in ERP
- wasteReasons: search waste reasons  in ERP
- productionRoutes: search production routes in ERP
- goodReceipts: search good receipts in ERP
- goodIssues: search good issues in ERP
- stockTransfers: search stock transfers in ERP
- inventoryCountings: search inventory countings in ERP
- productionOrders: search production orders in ERP
- productionSequences: search production sequences in ERO (production order + production route)
- productionPoints: insert production point in ERP (with or without time)
- stopPoints: insert stop point in ERP
- wastePoints: insert waste point in ERP

***

__Content Type__: all finAPI services use the “content-type” application/json for Parameters (body request) and Responses.

__Authentication__: finAPI uses Basic Authentication (user/password)

__Characteristics__: pagination, incremental query, default fields, objects and processes, use of custom fields (limited use), API usage and ERP transactions monitoring