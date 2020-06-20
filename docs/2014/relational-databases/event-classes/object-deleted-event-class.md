---
title: Object:Deleted, clase de eventos |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Object:Deleted event class
ms.assetid: d4db32bc-972d-4429-809a-a62047c33e79
author: stevestein
ms.author: sstein
ms.openlocfilehash: 90bcc20e16d775e6497958fc1adc58269fb24296
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029380"
---
# <a name="objectdeleted-event-class"></a>Object:Deleted, clase de eventos
  La clase de eventos Object:Deleted indica que se ha eliminado un objeto; por ejemplo, mediante instrucciones DROP INDEX y DROP TABLE. Esta clase de evento se puede utilizar para determinar si se están eliminando objetos; por ejemplo, con aplicaciones ODBC, que, a menudo, crean procedimientos almacenados temporales.  
  
 Al supervisar las columnas de datos predeterminadas LoginName y NTUserName, además de las clases de eventos Objects, puede determinar el nombre del usuario que crea, elimina o tiene acceso a objetos.  
  
## <a name="objectdeleted-event-class-data-columns"></a>Columnas de datos de la clase de evento Object:Deleted  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Yes|  
|EventClass|`int`|Tipo de evento = 47.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 0=Principio<br /><br /> 1=Confirmar<br /><br /> 2=Revertir|21|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IndexID|`int`|Id. del índice del objeto afectado por el evento. Para determinar el identificador de índice de un objeto, use la columna index_id de la vista de catálogo sys.indexes.|24|Yes|  
|IntegerData|`int`|Valor entero que depende de la clase de eventos capturada en el seguimiento.|25|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Yes|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|ObjectID|`int`|Identificador del objeto asignado por el sistema.|22|Sí|  
|ObjectID2|`bigint`|Id. de la entidad u objeto relacionado.|56|Yes|  
|ObjectName|`nvarchar`|Nombre del objeto al que se hace referencia.|34|Yes|  
|ObjectType|`int`|Valor que representa el tipo del objeto implicado en el evento. Este valor corresponde al de la columna Type de la tabla sys.objects. Para ver los valores, vea [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Yes|  
|RequestID|`int`|Identificador de la solicitud que contiene la instrucción.|49|Yes|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Yes|  
|XactSequence|`bigint`|Token que se utiliza para describir la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
