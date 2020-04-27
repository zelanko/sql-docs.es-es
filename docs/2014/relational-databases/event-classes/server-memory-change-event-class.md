---
title: Clase de eventos Server Memory Change | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Server Memory Change event class
ms.assetid: c9836484-39c5-4a89-b080-3567783b6fff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 358d468c900d367496cd904b4f401b0948af0853
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63044160"
---
# <a name="server-memory-change-event-class"></a>Server Memory Change [clase de eventos]
  La clase de eventos **Server Memory Change** se produce cuando el uso de memoria de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha aumentado o ha disminuido 1 megabyte (MB) o el 5 por ciento de la memoria máxima del servidor, el valor que sea más alto.  
  
## <a name="server-memory-change-event-class-data-columns"></a>Columnas de datos de la clase de eventos Server Memory Change  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Sí|  
|----------------------|---------------|-----------------|---------------|---------|  
|**EventClass**|**int**|Tipo de evento = 81.|27|No|  
|**EventSequence**|**int**|Secuencia de un evento determinado de la solicitud.|51|No|  
|**EventSubClass**|**int**|Tipo de la subclase de eventos.<br /><br /> 1=Aumento de memoria<br /><br /> 2=Disminución de memoria|21|Sí|  
|**IntegerData**|**int**|Nuevo tamaño de la memoria, en megabytes (MB).|25|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|**IdSolicitud**|**int**|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**TransactionID**|**bigint**|Id. de la transacción asignado por el sistema.|4|Sí|  
|**XactSequence**|**bigint**|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
