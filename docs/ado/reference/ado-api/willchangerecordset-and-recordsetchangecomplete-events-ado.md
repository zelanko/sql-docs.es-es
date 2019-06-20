---
title: Eventos WillChangeRecordset y RecordsetChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5ca84c5759523bf17c4e047b22cafbd48dce547
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710066"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventos WillChangeRecordset y RecordsetChangeComplete (ADO)
El **WillChangeRecordset** se llama al evento antes de que una operación pendiente cambie el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). El **RecordsetChangeComplete** se llama al evento después de la **Recordset** ha cambiado.  
  
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
  
 Cuando **RecordsetChangeComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, **adStatusErrorsOccurred** si el error, en la operación o **adStatusCancel** si la operación asociada con la ha aceptado anteriormente **WillChangeRecordset** se ha cancelado el evento.  
  
 Antes de **WillChangeRecordset** devuelve, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente o al establecer este parámetro en adStatusUnwantedEvent para impedir posteriores notificaciones.  
  
 Antes de **WillChangeRecordset** o **RecordsetChangeComplete** devuelve, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *pRecordset*  
 Un **Recordset** objeto. El **Recordset** para que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 Un **WillChangeRecordset** o **RecordsetChangeComplete** evento puede producirse porque el **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) o [Abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos.  
  
 Si el proveedor no admite marcadores, un **RecordsetChange** notificación de eventos se produce cada vez que se recuperan filas nuevas del proveedor. La frecuencia de este evento depende el **RecordsetCacheSize** propiedad.  
  
 Debe establecer el **adStatus** parámetro **adStatusUnwantedEvent** para cada posible **adReason** valor para detener completamente la notificación de eventos para cualquier evento que incluye un **adReason** parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
