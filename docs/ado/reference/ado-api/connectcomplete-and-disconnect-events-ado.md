---
description: Eventos ConnectComplete y Disconnect (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: db04bbeed12f9097768763024270ece7275d5c3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444547"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>Eventos ConnectComplete y Disconnect (ADO)
El evento **ConnectComplete** se llama después de que se inicie una conexión. Se llama al evento **Disconnect** una vez finalizada la conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un objeto de [error](../../../ado/reference/ado-api/error-object.md) . Describe el error que se produjo si el valor de *adStatus* es **adStatusErrorsOccurred**; de lo contrario, no se establece.  
  
 *adStatus*  
 Valor de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) que siempre devuelve **adStatusOK**.  
  
 Cuando se llama a **ConnectComplete** , este parámetro se establece en **adStatusCancel** si un evento **WillConnect** ha solicitado la cancelación de la conexión pendiente.  
  
 Antes de que se devuelva un evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar las notificaciones posteriores. Sin embargo, al cerrar y volver a abrir la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) , se vuelven a producir estos eventos.  
  
 *pConnection*  
 Objeto de **conexión** para el que se aplica este evento.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
