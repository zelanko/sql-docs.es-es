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
ms.openlocfilehash: 25eef06b7e25538cb874d99af98aee95495b95ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932330"
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
  
 *Statu*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) . Si se produce una advertencia, *adStatus* se establece en **AdStatusOK** y el *perror* contiene la advertencia.  
  
 Antes de que se devuelva este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pConnection*  
 Objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) . La conexión para la que se produjo la advertencia. Por ejemplo, se pueden producir advertencias al abrir un objeto de **conexión** o ejecutar un [comando](../../../ado/reference/ado-api/command-object-ado.md) en una **conexión**.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
