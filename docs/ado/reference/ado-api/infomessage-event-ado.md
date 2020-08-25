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
ms.openlocfilehash: 4cab5acb3ccedb9a1e42426da3701bc015f0ec2d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774834"
---
# <a name="infomessage-event-ado"></a>Evento InfoMessage (ADO)
Se llama al evento **InfoMessage** siempre que se produce una advertencia durante una operación **ConnectionEvent** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pError*  
 Un objeto de [error](./error-object.md) . Este parámetro contiene los errores que se devuelven. Si se devuelven varios errores, enumere la colección de **errores** para encontrarlos.  
  
 *adStatus*  
 Valor de estado de [EventStatusEnum](./eventstatusenum.md) . Si se produce una advertencia, *adStatus* se establece en **AdStatusOK** y el *perror* contiene la advertencia.  
  
 Antes de que se devuelva este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pConnection*  
 Objeto de [conexión](./connection-object-ado.md) . La conexión para la que se produjo la advertencia. Por ejemplo, se pueden producir advertencias al abrir un objeto de **conexión** o ejecutar un [comando](./command-object-ado.md) en una **conexión**.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](./connection-object-ado.md)