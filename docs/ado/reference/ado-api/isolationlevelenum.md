---
title: IsolationLevelEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b7f159568be94e20260809e05d2234e0274e29c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Especifica el nivel de aislamiento de transacción para un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|Indica que el proveedor utiliza un nivel de aislamiento diferente del especificado, pero que no se puede determinar el nivel.|  
|**adXactChaos**|16|Indica que no se puede sobrescribir los cambios de las transacciones más aisladas pendientes.|  
|**adXactBrowse**|256|Indica que, desde una transacción puede ver cambios no confirmados en otras transacciones.|  
|**adXactReadUncommitted**|256|Igual que **adXactBrowse**.|  
|**adXactCursorStability**|4096|Indica que de una transacción puede ver cambios en otras transacciones sólo después de que se han confirmado.|  
|**adXactReadCommitted**|4096|Igual que **adXactCursorStability**.|  
|**adXactRepeatableRead**|65536|Indica que en una transacción, no puede ver los cambios realizados en otras transacciones, pero que volver a consultar puede recuperar nuevos **Recordset** objetos.|  
|**adXactIsolated**|1048576|Indica que las transacciones se llevan a cabo de forma aislada de otras transacciones.|  
|**adXactSerializable**|1048576|Igual que **adXactIsolated**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)
