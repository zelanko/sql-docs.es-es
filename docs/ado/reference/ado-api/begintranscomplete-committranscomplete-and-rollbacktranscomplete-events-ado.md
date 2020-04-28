---
title: Eventos BeginTrans, CommitTrans y RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 750e89e97eb916c7db23e71475b753a57a4d90e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920442"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>Eventos BeginTransComplete, CommitTransComplete y RollbackTransComplete (ADO)
Se llamará a estos eventos después de que la operación asociada en el objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) termine de ejecutarse.  
  
-   Se llama a **BeginTransComplete** después de la operación [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   Se llama a **CommitTransComplete** después de la operación [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
-   Se llama a **RollbackTransComplete** después de la operación [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *TransactionLevel*  
 Un valor **Long** que contiene el nuevo nivel de transacción de los **BeginTrans** que produjeron este evento.  
  
 *pError*  
 Un objeto de [error](../../../ado/reference/ado-api/error-object.md) . Describe el error que se produjo si el valor de EventStatusEnum es **adStatusErrorsOccurred**; de lo contrario, no se establece.  
  
 *adStatus*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Cuando se llama a cualquiera de estos eventos, este parámetro se establece en **adStatusOK** si la operación que causó el evento se realizó correctamente, o en **adStatusErrorsOccurred** si se produjo un error en la operación.  
  
 Estos eventos pueden impedir las siguientes notificaciones si se establece este parámetro en **adStatusUnwantedEvent** antes de que el evento vuelva.  
  
 *pConnection*  
 Objeto de **conexión** para el que se produjo este evento.  
  
## <a name="remarks"></a>Observaciones  
 En Visual C++, varias **conexiones** pueden compartir el mismo método de control de eventos. El método utiliza el objeto de **conexión** devuelto para determinar qué objeto provocó el evento.  
  
 Si la propiedad [attributes](../../../ado/reference/ado-api/attributes-property-ado.md) se establece en **adXactCommitRetaining** o **adXactAbortRetaining**, se inicia una nueva transacción después de confirmar o revertir una transacción. Use el evento **BeginTransComplete** para omitir todos los eventos, excepto el primer evento de inicio de la transacción.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Ejemplo de los métodos BeginTrans, CommitTrans y RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans y RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
