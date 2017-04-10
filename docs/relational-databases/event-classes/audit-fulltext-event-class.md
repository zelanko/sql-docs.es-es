---
title: "Clase de eventos Audit Fulltext | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 95e4c5fd-e16f-446e-b42b-105495a8f39a
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Clase de eventos Audit Fulltext
  La clase de eventos **Audit Fulltext** se produce cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta y comunica con el proceso del demonio de filtro de texto completo.  
  
## Columnas de datos de la clase de eventos Audit Fulltext  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**Error**|**int**|Número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , si este evento informa de un error.|31|Sí|  
|**EventSequence**|**int**|Secuencia de un evento determinado dentro de la solicitud.|51|No|  
|**EventSubClass**|**int**|Tipo de conexión usada por el inicio de sesión. 1 = No agrupada, 2 = Agrupada.|21|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**Correcto**|**int**|1 = correcto. 0 = error Por ejemplo, el valor 1 significa que se ha comprobado un permiso correctamente y el valor 0 indica que se ha producido un error en la comprobación.|23|Sí|  
|**TargetLoginName**|**int**|Para acciones dirigidas a un inicio de sesión (por ejemplo, agregar un nuevo inicio de sesión), el nombre del inicio de sesión de destino.|42|Sí|  
|**TargetLoginSid**|**int**|Para acciones dirigidas a un inicio de sesión (por ejemplo, agregar un nuevo inicio de sesión), el número de identificación de seguridad (SID) del inicio de sesión de destino.|43|Sí|  
|**TextData**|**ntext**|Información de texto sobre el evento Full-Text. Normalmente este campo proporciona información sobre la conexión entre el proceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el proceso del demonio de filtro de texto completo|1|Sí|  
  
## Vea también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  