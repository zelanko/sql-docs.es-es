---
title: Eventos WillChangeRecordset y RecordsetChangeComplete (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a103d1710f01403e8e199fc308369b4a9dc82c8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventos WillChangeRecordset y RecordsetChangeComplete (ADO)
El **WillChangeRecordset** evento se le llama antes de que una operación pendiente cambie el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). El **RecordsetChangeComplete** eventos se llama después de la **Recordset** ha cambiado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *adReason*  
 Un [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica el motivo de este evento. Su valor puede ser **adRsnRequery**, **adRsnResynch**, **adRsnClose o**, **adRsnOpen**.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando **WillChangeRecordset** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando **RecordsetChangeComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, **adStatusErrorsOccurred** si el error de la operación o **adStatusCancel** si la operación asociada anteriormente aceptado **WillChangeRecordset** se ha cancelado el evento.  
  
 Antes de **WillChangeRecordset** devuelve resultados, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente o al establecer este parámetro en adStatusUnwantedEvent para impedir posteriores notificaciones.  
  
 Antes de **WillChangeRecordset** o **RecordsetChangeComplete** devuelve resultados, establezca este parámetro en **adStatusUnwantedEvent** para impedir notificaciones posteriores.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error que se ha producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *Connection*  
 A **Recordset** objeto. El **conjunto de registros** para la que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 A **WillChangeRecordset** o **RecordsetChangeComplete** evento puede producirse porque el **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) o [Abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos.  
  
 Si el proveedor no admite marcadores, un **RecordsetChange** notificación de eventos se produce cada vez que se recuperan filas nuevas del proveedor. La frecuencia de este evento depende del **RecordsetCacheSize** propiedad.  
  
 Debe establecer el **adStatus** parámetro **adStatusUnwantedEvent** para cada posible **adReason** valor para detener completamente la notificación de eventos para cualquier evento que incluya un **adReason** parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
