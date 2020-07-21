---
title: Clase de eventos SP:CacheHit | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:CacheHit event class
ms.assetid: 396aa22a-4723-47f5-ae72-7de99d92dd6f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ffc477b299daeda004cca26d95f3d33e2e5509b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85028464"
---
# <a name="spcachehit-event-class"></a>SP:CacheHit, clase de eventos
  La clase de eventos SP:CacheHit indica que un procedimiento almacenado se encuentra en la caché del plan.  
  
## <a name="spcachehit-event-class-data-columns"></a>Columnas de datos de la clase de evento SP:CacheHit  
  
|Nombre de columna de datos|`Data type`|Descripción|Identificador de columna|Filtrable|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Yes|  
|DatabaseID|`int`|Id. de la base de datos en que se ejecuta el procedimiento almacenado. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta el procedimiento almacenado.|35|Sí|  
|EventClass|`int`|Tipo de evento = 38.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado dentro de la solicitud.|51|No|  
|EventSubClass|`int`|Tipos de subclase de evento.<br /><br /> 1=Acierto de contexto de ejecución: Se encontró un plan de ejecución libre en la caché del plan.<br /><br /> 2=Acierto de compilación: Se encontró un plan compilado en la caché del plan.|21|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|ObjectID|`int`|Identificador asignado por el sistema del procedimiento almacenado encontrado en la caché.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto que se ha encontrado en la caché. Si ObjectName está lleno, TextData no se rellenará.|34|Sí|  
|ObjectType|`int`|Valor que representa el tipo del objeto implicado en el evento. Este valor corresponde al de la columna Type de la vista de catálogo sys.objects. Para ver los valores, vea [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Yes|  
|RequestID|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Texto del código SQL que se ha encontrado en la caché. Si TextData está lleno, ObjectName no se rellenará.|1|Yes|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
