---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c37a7385cc3aabb725f86261203d22b5b10c3be6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918873"
---
# <a name="eventreasonenum"></a>EventReasonEnum
Especifica el motivo por el que se produjo un evento que se produzca.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|Una operación de agrega un nuevo registro.|  
|**adRsnClose**|9|Una operación cerró el **Recordset**.|  
|**adRsnDelete**|2|Una operación de elimina un registro.|  
|**adRsnFirstChange**|11|Una operación realiza el primer cambio en un registro.|  
|**adRsnMove**|10|Una operación de mover el puntero de registro dentro de la **Recordset**.|  
|**adRsnMoveFirst**|12|Una operación de mover el puntero de registro en el primer registro de la **Recordset**.|  
|**adRsnMoveLast**|15|Una operación de mover el puntero de registro al último registro en el **Recordset**.|  
|**adRsnMoveNext**|13|Una operación de mover el puntero de registro al registro siguiente en el **Recordset**.|  
|**adRsnMovePrevious**|14|Una operación de mover el puntero de registro al registro anterior en el **Recordset**.|  
|**adRsnRequery**|7|Una operación vuelve a consultar el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adRsnResynch**|8|Una operación de volver a sincronizar la **Recordset** con la base de datos.|  
|**adRsnUndoAddNew**|5|Una operación de revertir la adición de un nuevo registro.|  
|**adRsnUndoDelete**|6|La eliminación de un registro puede revertir una operación.|  
|**adRsnUndoUpdate**|4|Una operación de revertir la actualización de un registro.|  
|**adRsnUpdate**|3|Una operación actualiza un registro existente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
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
