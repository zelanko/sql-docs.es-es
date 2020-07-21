---
title: Clases de eventos configurables por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- User-Configurable event class
ms.assetid: 06fe5f07-a0dd-4968-b123-56b124a86020
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3a166889694e6d4348587ca65f238f9a817f36f1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051394"
---
# <a name="user-configurable-event-class"></a>clases de eventos configurables por el usuario
  Utilice las categorías de eventos configurables por el usuario para supervisar eventos definidos por el usuario. Cree clases de eventos definidas por el usuario para supervisar eventos cuya supervisión no es posible con las clases de eventos suministradas por el sistema que pertenecen a otras categorías de eventos. Por ejemplo, se puede crear un evento definido por el usuario para supervisar el progreso de la aplicación que se está probando. A medida que se ejecuta la aplicación, pueden generarse eventos en los puntos predefinidos, lo que permite determinar el punto de ejecución actual de la aplicación.  
  
## <a name="user-configurable-event-class-data-columns"></a>Columnas de datos de las clases de eventos configurables por el usuario  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|BinaryData|`image`|Valor binario que depende de la clase de eventos que se captura en el seguimiento.|2|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|`int`|Tipo de evento = 82-91.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado dentro de la solicitud.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|RequestID|`int`|Id. de la solicitud que contiene la instrucción.|49|Sí|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Valor de texto que depende de la clase de eventos capturada en el seguimiento.|1|Yes|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)  
  
  
