---
title: EventReasonEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74e5f3debafb07a370a05e4cb7a2ffca07fae508
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="eventreasonenum"></a>EventReasonEnum
Especifica la razón por la que se produjo un evento que se produzca.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Una operación de agrega un nuevo registro.|  
|**adRsnClose o**|9|Una operación cerró el **conjunto de registros**.|  
|**adRsnDelete**|2|Una operación eliminó un registro.|  
|**adRsnFirstChange**|11|Una operación realiza el primer cambio en un registro.|  
|**adRsnMove**|10|Una operación de mover el puntero del registro en el **conjunto de registros**.|  
|**adRsnMoveFirst**|12|Una operación movió el puntero de registro al primer registro en el **conjunto de registros**.|  
|**adRsnMoveLast**|15|Una operación movió el puntero de registro al último registro en el **conjunto de registros**.|  
|**adRsnMoveNext**|13|Una operación de mover el puntero del registro en el registro siguiente en el **conjunto de registros**.|  
|**adRsnMovePrevious**|14|Una operación movió el puntero de registro al registro anterior en el **conjunto de registros**.|  
|**adRsnRequery**|7|Una operación volvió a consultar el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Una operación de volver a sincronizar la **Recordset** con la base de datos.|  
|**adRsnUndoAddNew**|5|Una operación revocó la adición de un nuevo registro.|  
|**adRsnUndoDelete**|6|Una operación deshacer la eliminación de un registro.|  
|**adRsnUndoUpdate**|4|Una operación revocó la actualización de un registro.|  
|**adRsnUpdate**|3|Una operación actualizó un registro existente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Eventos WillChangeRecord y RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[Eventos WillChangeRecordset y RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[Eventos WillMove y MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
