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
author: rothja
ms.author: jroth
ms.openlocfilehash: 90bfb1c947c02540d07c3cbc11e45436f8bd4a58
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764476"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>Eventos WillChangeRecordset y RecordsetChangeComplete (ADO)
Se llama al evento **WillChangeRecordset** antes de que una operación pendiente cambie el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). El evento **RecordsetChangeComplete** se llama después de que el **conjunto de registros** haya cambiado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *adReason*  
 Valor [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) que especifica el motivo de este evento. Su valor puede ser **adRsnRequery**, **adRsnResynch**, **adRsnClose**, **adRsnOpen**.  
  
 *adStatus*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 Cuando se llama a **WillChangeRecordset** , este parámetro se establece en **adStatusOK** si la operación que causó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando se llama a **RecordsetChangeComplete** , este parámetro se establece en **adStatusOK** si la operación que causó el evento se realizó correctamente, **adStatusErrorsOccurred** si se produjo un error en la operación o **adStatusCancel** si se ha cancelado la operación asociada al evento **WillChangeRecordset** previamente aceptado.  
  
 Antes de que **WillChangeRecordset** vuelva, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente o establezca este parámetro en adStatusUnwantedEvent para evitar notificaciones posteriores.  
  
 Antes de que se devuelva **WillChangeRecordset** o **RecordsetChangeComplete** , establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pError*  
 Un objeto de [error](../../../ado/reference/ado-api/error-object.md) . Describe el error que se produjo si el valor de *adStatus* es **adStatusErrorsOccurred**; de lo contrario, no se establece.  
  
 *pRecordset*  
 Objeto de **conjunto de registros** . **Conjunto de registros** para el que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 Puede producirse un evento **WillChangeRecordset** o **RecordsetChangeComplete** debido a la [reconsulta](../../../ado/reference/ado-api/requery-method.md) o a los métodos [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) del **conjunto de registros** .  
  
 Si el proveedor no admite marcadores, se produce una notificación de evento **RecordsetChange** cada vez que se recuperan nuevas filas del proveedor. La frecuencia de este evento depende de la propiedad **RecordsetCacheSize** .  
  
 Debe establecer el parámetro **adStatus** en **adStatusUnwantedEvent** para cada valor de **adReason** posible para detener por completo la notificación de eventos para cualquier evento que incluya un parámetro **adReason** .  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
