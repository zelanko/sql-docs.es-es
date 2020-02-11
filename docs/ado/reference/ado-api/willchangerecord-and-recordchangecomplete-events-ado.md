---
title: Eventos WillChangeRecord y RecordChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e632db34fbbacbee61cd943067052af27a8cfe8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938673"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>Eventos WillChangeRecord y RecordChangeComplete (ADO)
Se llama al evento **WillChangeRecord** antes de que cambien uno o más registros (filas) del [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) . Se llama al evento **RecordChangeComplete** después de que uno o varios registros cambien.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Reason*  
 Valor [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) que especifica el motivo de este evento. Su valor puede ser **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**o **adRsnFirstChange**.  
  
 *cRecords*  
 Un valor **Long** que indica el número de registros que cambian (se ven afectados).  
  
 *pError*  
 Un objeto de [error](../../../ado/reference/ado-api/error-object.md) . Describe el error que se produjo si el valor de *adStatus* es **adStatusErrorsOccurred**; de lo contrario, no se establece.  
  
 *Statu*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Cuando se llama a **WillChangeRecord** , este parámetro se establece en **adStatusOK** si la operación que causó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando se llama a **RecordChangeComplete** , este parámetro se establece en **adStatusOK** si la operación que causó el evento se realizó correctamente, o en **adStatusErrorsOccurred** si se produjo un error en la operación.  
  
 Antes de que se devuelva **WillChangeRecord** , establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación que provocó este evento o establecer este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 Antes de que se devuelva **RecordChangeComplete** , establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pRecordset*  
 Objeto de **conjunto de registros** . **Conjunto de registros** para el que se produjo este evento.  
  
## <a name="remarks"></a>Observaciones  
 Es posible que se produzca un evento **WillChangeRecord** o **RecordChangeComplete** para el primer campo modificado de una fila debido a las siguientes operaciones de **conjunto de registros** : [Update](../../../ado/reference/ado-api/update-method.md), [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)y [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). El valor de [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) del **conjunto de registros** determina qué operaciones hacen que se produzcan los eventos.  
  
 Durante el evento **WillChangeRecord** , la propiedad del [filtro](../../../ado/reference/ado-api/filter-property.md) del **conjunto de registros** se establece en **adFilterAffectedRecords**. No se puede cambiar esta propiedad mientras se procesa el evento.  
  
 Debe establecer el parámetro **adStatus** en **adStatusUnwantedEvent** para cada valor de **adReason** posible para detener por completo la notificación de eventos para cualquier evento que incluya un parámetro **adReason** .  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
