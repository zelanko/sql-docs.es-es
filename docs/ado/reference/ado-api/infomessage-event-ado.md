---
title: El evento InfoMessage (ADO) | Documentos de Microsoft
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
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f1e479b4dfb5b9cb557030e03afeac3f6278720
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
El **InfoMessage** eventos se llama cada vez que se produce una advertencia durante una **ConnectionEvent** operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Este parámetro contiene los errores que se devuelven. Si se devuelven varios errores, enumere el **errores** colección para encontrarlos.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado. Si se produce una advertencia, *adStatus* está establecido en **adStatusOK** y *pError* contiene la advertencia.  
  
 Antes de que se devuelve este evento, establezca este parámetro en **adStatusUnwantedEvent** para impedir notificaciones posteriores.  
  
 *pConnection*  
 A [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. La conexión para el que se produjo la advertencia. Por ejemplo, las advertencias pueden ocurrir al abrir un **conexión** objeto o ejecutar un [comando](../../../ado/reference/ado-api/command-object-ado.md) en un **conexión**.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

