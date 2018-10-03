---
title: Clase de eventos SP:Recompile |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d92673f3b551076eea675e9a5d909acd5f293337
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060905"
---
# <a name="sprecompile-event-class"></a>SP:Recompile, clase de eventos
  La clase de eventos SP:Recompile indica que un procedimiento almacenado, desencadenador o función definida por el usuario se ha vuelto a compilar. Las recompilaciones notificadas por esta clase de eventos se producen en el nivel de instrucción.  
  
 La forma preferida de realizar un seguimiento de las recompilaciones de nivel de instrucción consiste en usar la clase de eventos SQL:StmtRecompile. La clase de eventos SP:Recompile está en desuso. Para más información, consulte [SQL:StmtRecompile Event Class](sql-stmtrecompile-event-class.md).  
  
## <a name="sprecompile-event-class-data-columns"></a>Columnas de datos de la clase de eventos SP:Recompile  
  
|Nombre de columna de datos|`Data type`|Descripción|Identificador de columna|Filtrable|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se llena si el cliente proporciona el Id. de proceso.|9|Sí|  
|DatabaseID|`int`|Id. de la base de datos en que se ejecuta el procedimiento almacenado. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta el procedimiento almacenado.|35|Sí|  
|EventClass|`int`|Tipo de evento = 37.|27|no|  
|EventSequence|`int`|Secuencia de un evento determinado dentro de la solicitud.|51|no|  
|EventSubClass|`int`|Tipo de la subclase de eventos. Indica la razón de la recompilación.<br /><br /> 1 = Cambio en el esquema<br /><br /> 2 = Cambio en estadísticas<br /><br /> 3 = Recompilación DNR<br /><br /> 4 = Cambio en opción configurada<br /><br /> 5 = Cambio en tabla Temp<br /><br /> 6 = Cambio en conjunto de filas remoto<br /><br /> 7 = Cambio en permisos For Browse<br /><br /> 8 = Cambio en entorno de notificación de consultas<br /><br /> 9 = Cambio en vista MPI<br /><br /> 10 = Cambio en opciones de cursor<br /><br /> 11 = Opción con recompilación|21|Sí|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IntegerData2|`int`|Desplazamiento final de la instrucción en el procedimiento almacenado o proceso por lotes que causó la recompilación. El desplazamiento final es -1 si la instrucción es la última de su lote.|55|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NestLevel|`int`|Nivel de anidamiento del procedimiento almacenado.|29|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ObjectID|`int`|Identificador asignado por el sistema al procedimiento almacenado.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto que ha desencadenado la recompilación.|34|Sí|  
|ObjectType|`int`|Valor que representa el tipo de objeto implicado en el evento. Para más información, consulte [ObjectType Trace Event Column](objecttype-trace-event-column.md).|28|Sí|  
|Offset|`int`|Desplazamiento inicial de la instrucción en el procedimiento almacenado o proceso por lotes que causó la recompilación.|61|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|no|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|SqlHandle|`varbinary`|Hash de 64 bits basado en el texto de una consulta ad hoc o en el Id. de base de datos y de objeto de un objeto SQL. Este valor puede pasarse a sys.dm_exec_sql_text para recuperar el texto SQL asociado.|63|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Texto de la instrucción Transact-SQL que causó la recompilación de nivel de instrucción.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que se utiliza para describir la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SQL:StmtRecompile (clase de eventos)](sql-stmtrecompile-event-class.md)  
  
  
