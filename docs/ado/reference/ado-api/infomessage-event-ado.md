---
title: Evento InfoMessage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 516e6a95ba98f1b8d66ddf9f417460ef2a6b7dc0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602573"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
El **InfoMessage** se llama al evento cada vez que se produce una advertencia durante una **ConnectionEvent** operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Este parámetro contiene los errores que se devuelven. Si se devuelven varios errores, enumere el **errores** colección para encontrarlos.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado. Si se produce una advertencia, *adStatus* está establecido en **adStatusOK** y *pError* contiene la advertencia.  
  
 Antes de que se devuelve este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pConnection*  
 Un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. La conexión para el que se produjo la advertencia. Por ejemplo, las advertencias pueden ocurrir al abrir un **conexión** objeto o ejecutar un [comando](../../../ado/reference/ado-api/command-object-ado.md) en un **conexión**.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
