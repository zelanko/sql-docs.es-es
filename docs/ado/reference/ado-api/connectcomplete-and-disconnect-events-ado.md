---
title: Eventos ConnectComplete y Disconnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 448270ddf0e8cd7efb5ec39a93d4ff993360730e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919578"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>Eventos ConnectComplete y Disconnect (ADO)
El **ConnectComplete** se llama al evento después de inicia una conexión. El **desconexión** se llama al evento después de que finalice una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de *adStatus* es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor que siempre devuelve **adStatusOK**.  
  
 Cuando **ConnectComplete** es llama, este parámetro se establece en **adStatusCancel** si un **WillConnect** evento ha solicitado la cancelación de la conexión pendiente.  
  
 Antes de que se devuelva cualquier evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores. Sin embargo, cerrar y volver a abrir el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) hace que estos eventos se vuelve a producir.  
  
 *pConnection*  
 El **conexión** el objeto para el que se aplica este evento.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
