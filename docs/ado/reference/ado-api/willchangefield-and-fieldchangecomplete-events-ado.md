---
title: Eventos WillChangeField y FieldChangeComplete (ADO) | Documentos de Microsoft
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
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d9ce0412a76f34f653273d294e7f8add031a9d9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>Eventos WillChangeField y FieldChangeComplete (ADO)
El **WillChangeField** evento se le llama antes de que una operación pendiente cambie el valor de uno o varios [campo](../../../ado/reference/ado-api/field-object.md) objetos en el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). El **FieldChangeComplete** eventos se llama después del valor de uno o varios **campo** objetos ha cambiado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *cFields*  
 A **largo** que indica el número de **campo** objetos de *campos*.  
  
 *Campos*  
 Para **WillChangeField**, *campos* parámetro es una matriz de **variantes** que contiene **campo** objetos con los valores originales. Para **FieldChangeComplete**, *campos* parámetro es una matriz de **variantes** que contiene **campo** objetos con los valores cambiados .  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error que se ha producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando **WillChangeField** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando **FieldChangeComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si Error en la operación.  
  
 Antes de **WillChangeField** devuelve resultados, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente.  
  
 Antes de **FieldChangeComplete** devuelve resultados, establezca este parámetro en **adStatusUnwantedEvent** para impedir notificaciones posteriores.  
  
 *Connection*  
 A **Recordset** objeto. El **conjunto de registros** para la que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 A **WillChangeField** o **FieldChangeComplete** evento puede ocurrir cuando se establece la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad y llamar a la [actualización](../../../ado/reference/ado-api/update-method.md) (método) con parámetros de matriz de campo y valor.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)
