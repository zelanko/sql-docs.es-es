---
title: Deadlock Graph, clase de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Deadlock Graph event class
ms.assetid: 20f92233-c912-4382-8993-8e2e23d03fbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 741fb8ac694568911c1b2b5def7bd07a8c86e8ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662923"
---
# <a name="deadlock-graph-event-class"></a>Deadlock Graph, clase de eventos
  La clase de eventos **Deadlock Graph** proporciona la descripción en formato XML de un interbloqueo. Esta clase de eventos se produce al mismo tiempo que la clase de eventos **Lock:Deadlock** .  
  
## <a name="deadlock-graph-event-class-data-columns"></a>Columnas de datos de la clase de eventos Deadlock Graph  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|Tipo de evento = 148.|27|Sin|  
|**EventSequence**|**int**|Secuencia de un evento determinado de la solicitud.|51|Sin|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario. El valor para esta clase de eventos siempre es 1.|60|Sí|  
|**LoginName**|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario). Este valor siempre es el usuario de sistema de este evento.|11|Sí|  
|**LoginSid**|**image**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor. Este valor siempre es el SID del usuario de sistema de este evento.|41|Sí|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se detectó el interbloqueo.|14|Sí|  
|**TextData**|**ntext**|Descripción en formato XML del interbloqueo.|1|Sí|  
|**TransactionID**|**bigint**|No se usa.|4|Sí|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Lock:Deadlock (clase de eventos)](lock-deadlock-event-class.md)  
  
  
