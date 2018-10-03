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
manager: craigg
ms.openlocfilehash: dd31a75a45bd38bda04655bbb47daca09714803c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822024"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>Eventos WillChangeRecord y RecordChangeComplete (ADO)
El **WillChangeRecord** se llama al evento antes de uno o más registros (filas) el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) cambiar. El **RecordChangeComplete** se llama al evento después de que uno o más registros de cambian.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *adReason*  
 Un [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica el motivo de este evento. Su valor puede ser **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, o **adRsnFirstChange**.  
  
 *cRecords*  
 Un **largo** valor que indica el número de registros cambiados (afectados).  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando **WillChangeRecord** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando **RecordChangeComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si Error en la operación.  
  
 Antes de **WillChangeRecord** devuelve, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación que provocó este evento o establezca este parámetro en  **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 Antes de **RecordChangeComplete** devuelve, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pRecordset*  
 Un **Recordset** objeto. El **Recordset** para que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 Un **WillChangeRecord** o **RecordChangeComplete** evento puede producirse por el primer campo modificado en una fila debido a lo siguiente **Recordset** operations: [ Actualización](../../../ado/reference/ado-api/update-method.md), [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), y [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). El valor de la **Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) determina qué operaciones hacen que se producen los eventos.  
  
 Durante la **WillChangeRecord** eventos, el **Recordset** [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad está establecida en **adFilterAffectedRecords**. No se puede cambiar esta propiedad al procesar el evento.  
  
 Debe establecer el **adStatus** parámetro **adStatusUnwantedEvent** para cada posible **adReason** valor para detener completamente la notificación de eventos para cualquier evento que incluye un **adReason** parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
