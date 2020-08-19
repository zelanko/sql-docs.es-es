---
description: Evento InfoMessage (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d3957c6cf6843ba27c54fb5a979901bd4a656c2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443457"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
Se llama al evento **InfoMessage** siempre que se produce una advertencia durante una operación **ConnectionEvent** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un objeto de [error](../../../ado/reference/ado-api/error-object.md) . Este parámetro contiene los errores que se devuelven. Si se devuelven varios errores, enumere la colección de **errores** para encontrarlos.  
  
 *adStatus*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Si se produce una advertencia, *adStatus* se establece en **AdStatusOK** y el *perror* contiene la advertencia.  
  
 Antes de que se devuelva este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pConnection*  
 Objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) . La conexión para la que se produjo la advertencia. Por ejemplo, se pueden producir advertencias al abrir un objeto de **conexión** o ejecutar un [comando](../../../ado/reference/ado-api/command-object-ado.md) en una **conexión**.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
