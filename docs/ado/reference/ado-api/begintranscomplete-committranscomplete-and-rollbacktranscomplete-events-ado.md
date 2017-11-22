---
title: Eventos de BeginTrans, CommitTrans y RollbackTrans (ADO) | Documentos de Microsoft
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
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 782e17249205d2619fc5aa4c0699166fc21f7c78
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>Eventos BeginTransComplete, CommitTransComplete y RollbackTransComplete eventos (ADO)
Estos eventos se les llama después de la operación asociada en el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto termina de ejecutarse.  
  
-   **Eventos BeginTransComplete** se llama después de la [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operación.  
  
-   **CommitTransComplete** se llama después de la [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operación.  
  
-   **RollbackTransComplete** se llama después de la [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *TransactionLevel*  
 A **largo** valor que contiene el nuevo nivel de transacción de la **BeginTrans** que produjo este evento.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error que se ha producido si el valor de EventStatusEnum es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado. Cuando se llama a cualquiera de estos eventos, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si la operación produce un error.  
  
 Estos eventos pueden impedir notificaciones posteriores si se establece este parámetro **adStatusUnwantedEvent** antes de que el evento vuelva.  
  
 *pConnection*  
 El **conexión** el objeto para el que se produjo este evento.  
  
## <a name="remarks"></a>Comentarios  
 En Visual C++, varios **conexiones** pueden compartir el mismo método de control de eventos. El método usa el valor devuelto **conexión** para determinar qué objeto causó el evento.  
  
 Si el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad está establecida en **adXactCommitRetaining** o **adXactAbortRetaining**, inicia una nueva transacción después de confirmar o revertir una transacción. Use la **BeginTransComplete** evento para pasar por alto todas, pero el primer evento de inicio de la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans y ejemplo de los métodos RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Métodos BeginTrans, CommitTrans y RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
