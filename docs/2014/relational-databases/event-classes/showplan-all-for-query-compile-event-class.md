---
title: Clase de eventos Showplan All for Query Compile | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan All for Query Compile event class
ms.assetid: bb1dc446-5e6c-43d6-9db8-78c76cc2e01f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6a093432acae5f2ac41a9a8136db047130d7548c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85028539"
---
# <a name="showplan-all-for-query-compile-event-class"></a>Showplan All for Query Compile [clase de eventos]
  La clase de eventos Showplan All for Query Compile se produce cuando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compila una instrucción SQL. Incluya esta clase de eventos para identificar los operadores Showplan. La información contenida es un subconjunto de la disponible en la clase de eventos Showplan XML For Query Compile.  
  
 La clase de eventos Showplan All for Query Compile muestra datos completos de tiempo de compilación, por lo que los seguimientos que incluyen Showplan All for Query Compile pueden afectar de forma considerable el rendimiento. Para minimizar este riesgo, limite el uso de esta clase de evento a los seguimientos que supervisan problemas específicos durante periodos breves.  
  
 Cuando se incluye la clase de eventos Showplan All for Query Compile en un seguimiento es preciso seleccionar la columna de datos BinaryData. Si no se incluye, la información de esta clase de eventos no se mostrará en el seguimiento.  
  
## <a name="showplan-all-for-query-compile-event-class-data-columns"></a>Columnas de datos de la clase de evento Showplan All For Query Compile  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|BinaryData|`image`|Costo estimado de la consulta.|2|No|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|`int`|Tipo de evento = 169.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado dentro de la solicitud.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IntegerData|`int`|Número estimado de filas devueltas.|25|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LineNumber|`int`|Muestra el número de la línea que contiene el error.|5|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Yes|  
|LoginSID|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|No|  
|NestLevel|`int`|Valor entero que representa los datos devueltos por @@NESTLEVEL.|29|Yes|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|ObjectID|`int`|Identificador del objeto asignado por el sistema.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto al que se hace referencia.|34|Yes|  
|ObjectType|`int`|Valor que representa el tipo del objeto implicado en el evento. Este valor corresponde al de la columna Type de la tabla sys.objects. Para ver los valores, vea [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Yes|  
|RequestID|`int`|Id. de la solicitud que contiene la instrucción.|49|Yes|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de proceso del servidor que asigna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al procesado relacionado con el cliente.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Yes|  
|XactSequence|`bigint`|Token que se utiliza para describir la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Referencia de operadores lógicos y físicos del plan de presentación](../showplan-logical-and-physical-operators-reference.md)  
  
  
