---
title: Eventos WillMove y MoveComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88a04ff636f06589515f409b7c2274217ae8f3f8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710018"
---
# <a name="willmove-and-movecomplete-events-ado"></a>Eventos WillMove y MoveComplete (ADO)
El **WillMove** se llama al evento antes de que una operación pendiente cambia la posición actual en el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). El **MoveComplete** se llama al evento después de la posición actual en el **Recordset** cambios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *adReason*  
 Un [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica el motivo de este evento. Su valor puede ser **adRsnMoveFirst**, **adRsnMoveLast**, **adRsnMoveNext**, **adRsnMovePrevious**, **adRsnMove** , o **adRsnRequery**.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece el parámetro.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando **WillMove** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando **MoveComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si el Error en la operación.  
  
 Antes de **WillMove** devuelve, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente, o establezca este parámetro en **adStatusUnwantedEvent** Para evitar notificaciones posteriores.  
  
 Antes de **MoveComplete** devuelve, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pRecordset*  
 Un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. El **Recordset** para que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 Un **WillMove** o **MoveComplete** evento puede producirse debido a lo siguiente **Recordset** operaciones: [Abra](../../../ado/reference/ado-api/open-method-ado-recordset.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), y [Requery](../../../ado/reference/ado-api/requery-method.md). Estos eventos pueden producirse debido a las siguientes propiedades: [Filtro](../../../ado/reference/ado-api/filter-property.md), [índice](../../../ado/reference/ado-api/index-property.md), [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), y [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md). Estos eventos también se producen si un niño **Recordset** tiene **Recordset** eventos conectados y el elemento primario **Recordset** se mueve.  
  
 Debe establecer el *adStatus* parámetro **adStatusUnwantedEvent** para cada posible *adReason* valor con el fin de detener completamente la notificación de eventos para cualquier evento que incluye un *adReason* parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
