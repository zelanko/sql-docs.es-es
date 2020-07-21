---
title: OLEDB Errors, clase de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Errors event class
ms.assetid: 0ce1e906-5d92-42f2-ab38-8771ad5ca008
author: stevestein
ms.author: sstein
ms.openlocfilehash: 97918f1be9c5256fe05c873841ceca98fff3917f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052853"
---
# <a name="oledb-errors-event-class"></a>OLEDB Errors, clase de eventos
  La clase de eventos OLEDB Errors se produce en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando una llamada a un proveedor OLE DB devuelve un error. Incluya esta clase de eventos en los seguimientos para ver un HRESULT con errores de un proveedor OLE DB.  
  
 Cuando se incluye la clase de eventos OLEDB Errors en un seguimiento, la cantidad de sobrecarga depende de la frecuencia con la que se producen errores del proveedor OLE DB en relación con la base de datos durante el seguimiento. Si se producen con frecuencia, puede que el seguimiento reduzca el rendimiento de forma significativa.  
  
## <a name="oledb-errors-event-class-data-columns"></a>Columnas de datos de la clase de eventos OLEDB Errors  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Yes|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Yes|  
|Error|`int`|HRESULT devuelto por el proveedor.|31|Sí|  
|EventClass|`int`|Tipo de evento = 61.|27|No|  
|EventSequence|`int`|Secuencia de la clase de eventos OLE DB en el lote.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LinkedServerName|`nvarchar`|Nombre del servidor vinculado.|45|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en formato DOMINIO\nombreDeUsuario).|11|Yes|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Yes|  
|MethodName|`nvarchar`|Nombre del método OLE DB.|47|Yes|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ProviderName|`nvarchar`|Nombre del proveedor OLE DB.|46|Yes|  
|RequestID|`int`|Identificador de la solicitud que contiene la instrucción.|49|Yes|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`nvarchar`|Parámetros enviados y recibidos en la llamada OLE DB.|1|No|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Yes|  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Objetos de automatización OLE en Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
