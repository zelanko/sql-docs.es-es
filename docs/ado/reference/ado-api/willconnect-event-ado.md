---
title: Evento WillConnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 01b5c20668f97c80ae5abdcbb213914c012c7359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710060"
---
# <a name="willconnect-event-ado"></a>Evento WillConnect (ADO)
El **WillConnect** se llama al evento antes de iniciar una conexión.  
  
 **Se aplica a:** [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Un **cadena** que contiene información de conexión para la conexión pendiente.  
  
 *UserID*  
 Un **cadena** que contiene un nombre de usuario para la conexión pendiente.  
  
 *Contraseña*  
 Un **cadena** que contiene una contraseña para la conexión pendiente.  
  
 *Opciones*  
 Un **largo** valor que indica cómo el proveedor debe evaluar el *ConnectionString*. La única opción es **adAsyncOpen**.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 Cuando se llama a este evento, este parámetro se establece en **adStatusOK** de forma predeterminada. Se establece en **adStatusCantDeny** si el evento no puede solicitar la cancelación de la operación pendiente.  
  
 Antes de que se devuelve este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores. Establezca este parámetro en **adStatusCancel** para solicitar la operación de conexión que provocó la cancelación de esta notificación.  
  
 *pConnection*  
 El [conexión](../../../ado/reference/ado-api/connection-object-ado.md) el objeto para el que se aplica esta notificación de eventos. Cambios en los parámetros de la **conexión** por la **WillConnect** controlador de eventos no tiene ningún efecto el **conexión**.  
  
## <a name="remarks"></a>Comentarios  
 Cuando **WillConnect** se llama, el *ConnectionString*, *UserID*, *contraseña*, y *opciones* los parámetros se establecen en los valores establecidos por la operación que provocó este evento (la conexión pendiente) y se puede cambiar antes de que el evento. **WillConnect** puede devolver una solicitud de cancelación de la conexión pendiente.  
  
 Cuando se cancela este evento, **ConnectComplete** se llamará con su *adStatus* parámetro establecido en **adStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
