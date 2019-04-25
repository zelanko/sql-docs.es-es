---
title: Eventos WillChangeField y FieldChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f046a3a33e05228ab5e49116bc46eb9451f43129
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642454"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>Eventos WillChangeField y FieldChangeComplete (ADO)
El **WillChangeField** se llama al evento antes de que una operación pendiente cambie el valor de uno o varios [campo](../../../ado/reference/ado-api/field-object.md) objetos en el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). El **FieldChangeComplete** se llama al evento posterior al valor de uno o varios **campo** objetos ha cambiado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *cFields*  
 Un **largo** que indica el número de **campo** objetos *campos*.  
  
 *Fields*  
 Para **WillChangeField**, *campos* parámetro es una matriz de **variantes** que contiene **campo** objetos con los valores originales. Para **FieldChangeComplete**, *campos* parámetro es una matriz de **variantes** que contiene **campo** objetos con los valores cambiados .  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando **WillChangeField** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente. Se establece en **adStatusCantDeny** si este evento no puede solicitar la cancelación de la operación pendiente.  
  
 Cuando **FieldChangeComplete** es llama, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si Error en la operación.  
  
 Antes de **WillChangeField** devuelve, establezca este parámetro en **adStatusCancel** para solicitar la cancelación de la operación pendiente.  
  
 Antes de **FieldChangeComplete** devuelve, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pRecordset*  
 Un **Recordset** objeto. El **Recordset** para que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 Un **WillChangeField** o **FieldChangeComplete** evento puede producirse cuando se establece la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad y una llamada a la [actualización](../../../ado/reference/ado-api/update-method.md) (método) con los parámetros de matriz de campo y el valor.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
