---
title: Clase de eventos SP:StmtStarting |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:StmtStarting event class
ms.assetid: 73550597-a3f3-4454-8678-0bf39db80a7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: a69956a87414c073a49e5a92e81c6b85ce5bb720
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85028354"
---
# <a name="spstmtstarting-event-class"></a>SP:StmtStarting, clase de eventos
  La clase de eventos SP:StmtStarting indica que se ha iniciado una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] dentro de un procedimiento almacenado.  
  
## <a name="spstmtstarting-event-class-data-columns"></a>Columnas de datos de la clase de evento SP:StmtStarting  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Yes|  
|DatabaseID|`int`|Id. de la base de datos en que se ejecuta el procedimiento almacenado. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta el procedimiento almacenado.|35|Yes|  
|EventClass|`int`|Tipo de evento = 44.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IntegerData2|`int`|Desplazamiento final (en bytes) de la instrucción que se está ejecutando.|55|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LineNumber|`int`|Número de línea de la instrucción que se está ejecutando.|5|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Yes|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Yes|  
|NestLevel|`int`|Valor entero que representa los datos devueltos por @@NESTLEVEL.|29|Yes|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|ObjectID|`int`|Identificador del objeto asignado por el sistema.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto al que se hace referencia.|34|Yes|  
|ObjectType|`int`|Valor que representa el tipo del objeto implicado en el evento. Este valor corresponde al de la columna Type de la vista de catálogo sys.objects. Para ver los valores, vea [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Yes|  
|Offset|`int`|Desplazamiento inicial de la instrucción en el procedimiento almacenado o lote.|61|Yes|  
|RequestID|`int`|Identificador de la solicitud que contiene la instrucción.|49|Yes|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SourceDatabaseID|`int`|Id. de la base de datos en la que está el objeto.|62|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|State|`int`|Indica si la instrucción se está ejecutando después de volver a compilar.<br /><br /> 1=Recompilada|30|Yes|  
|TextData|`ntext`|Valor de texto que depende de la clase de eventos capturada en el seguimiento.|1|Yes|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Yes|  
|XactSequence|`bigint`|Token que se utiliza para describir la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
