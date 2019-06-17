---
title: Clase de eventos SP:Completed |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:Completed event class
ms.assetid: 7636a433-5d32-4562-8f5a-694f8e2beeca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bcc8cdc62616dd26eb714b78ad07296a794b55f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63050971"
---
# <a name="spcompleted-event-class"></a>SP:Completed, clase de eventos
  La clase de eventos SP:Completed indica que el procedimiento almacenado ha terminado de ejecutarse.  
  
## <a name="spcompleted-event-class-data-columns"></a>Columnas de datos de la clase de evento SP:Completed  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|`int`|Id. de la base de datos en que se ejecuta el procedimiento almacenado. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta el procedimiento almacenado.|35|Sí|  
|Duration|`bigint`|Tiempo (en microsegundos) que tarda el evento.|13|Sí|  
|EndTime|`datetime`|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting.|15|Sí|  
|EventClass|`int`|Tipo de evento = 43.|27|Sin|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|Sin|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LineNumber|`int`|Muestra el número de línea de la instrucción de ejecución que llamó a este procedimiento almacenado.|5|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NestLevel|`int`|Nivel de anidamiento del procedimiento almacenado.|29|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ObjectID|`int`|Identificador asignado por el sistema al procedimiento almacenado.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto al que se hace referencia.|34|Sí|  
|ObjectType|`int`|Tipo de procedimiento almacenado al que se ha llamado. Este valor corresponde al de la columna Type de la vista de catálogo sys.objects. Para ver los valores, consulte [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|RowCounts|`bigint`|Número de filas de todas las instrucciones incluidas en este procedimiento almacenado.|48|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SourceDatabaseID|`int`|Id. de la base de datos en la que está el objeto.|62|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Texto de la llamada del procedimiento almacenado.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
