---
title: 'Clase de eventos Progress Report: Online Index Operation | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8f9d7aec25ce6ac24cf47d0c34f856e586fdce28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="progress-report-online-index-operation-event-class"></a>Progress Report: Online Index Operation (clase de eventos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La clase de eventos Progress Report: Online Index Operation indica el progreso de una operación de generación de índice en línea mientras el proceso de generación está en ejecución.  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>Columnas de datos de la clase de eventos Progress Report: Online Index Operation  
  
|Nombre de columna de datos|Tipo de datos|Description|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BigintData1|**bigint**|Número de filas insertadas.|52|Sí|  
|BigintData2|**bigint**|0 = plan serie; de lo contrario, identificador de subproceso durante la ejecución en paralelo.|53|Sí|  
|ClientProcessID|**int**|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|**int**|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|Duration|**bigint**|Tiempo (en microsegundos) que tarda el evento.|13|Sí|  
|EndTime|**datetime**|Hora a la que se completó la operación de índice en línea.|15|Sí|  
|EventClass|**int**|Tipo de evento = 190.|27|no|  
|EventSequence|**int**|Secuencia de un evento determinado de la solicitud.|51|no|  
|EventSubClass|**int**|Tipo de la subclase de eventos.<br /><br /> 1=Inicio<br /><br /> 2=Empieza la ejecución de la fase 1<br /><br /> 3=Finaliza la ejecución de la fase 1<br /><br /> 4=Empieza la ejecución de la fase 2<br /><br /> 5=Finaliza la ejecución de la fase 2<br /><br /> 6=Recuento de filas insertadas<br /><br /> 7=Listo<br /><br /> La fase 1 hace referencia al objeto base (índice clúster o montón) o si la operación del índice solo implica a un índice no clúster. La fase 2 se usa cuando una operación de compilación de índice implica tanto al índice original recompilado como a índices no clúster adicionales.  Por ejemplo, si un objeto tiene un índice clúster y varios índices no clúster, 'rebuild all' recompilaría todos los índices. El objeto base (el índice clúster) se recompila en la fase 1 y, a continuación, todos los índices no clúster se recompilan en la fase 2.|21|Sí|  
|GroupID|**int**|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IndexID|**int**|Id. del índice del objeto afectado por el evento.|24|Sí|  
|IsSystem|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|**nvarchar**|Nombre del usuario de Windows.|6|Sí|  
|ObjectID|**int**|Identificador del objeto asignado por el sistema.|22|Sí|  
|ObjectName|**nvarchar**|Nombre del objeto al que se hace referencia.|34|Sí|  
|PartitionId|**bigint**|Identificador de la partición que se está generando.|65|Sí|  
|PartitionNumber|**int**|Número normal de la partición que se está generando.|25|Sí|  
|ServerName|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|no|  
|SessionLoginName|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|**datetime**|Hora a la que se inició el evento.|14|Sí|  
|TransactionID|**bigint**|Id. de la transacción asignado por el sistema.|4|Sí|  
  
## <a name="see-also"></a>Ver también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
