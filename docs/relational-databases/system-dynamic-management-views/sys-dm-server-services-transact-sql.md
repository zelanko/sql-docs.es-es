---
title: sys.dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8acb2fae0aa0edadf1995a0a103ff60b66a912a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686225"
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre los servicios SQL Server, Texto completo y Agente SQL Server en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta vista de administración dinámica para notificar información de estado sobre estos servicios.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Nombre de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], servicio Agente SQL Server o texto completo. No puede ser null.|  
|startup_type|**int**|Indica el modo de inicio del servicio. Los siguientes son los valores posibles y sus correspondientes descripciones.<br /><br /> 0: Otros<br />1: Otros<br />2: Automático<br />3: Manual<br />4: Deshabilitado<br /><br /> Acepta valores NULL.|  
|startup_desc|**nvarchar(256)**|Describe el modo de inicio del servicio. Los siguientes son los valores posibles y sus correspondientes descripciones.<br /><br /> Otro: Otro (inicio de arranque)<br />Otro: Otro (inicio del sistema)<br />Automático: Inicio automático<br />Manual: Inicio a petición<br />Deshabilitado: Deshabilitado<br /><br /> No puede ser null.|  
|status|**int**|Indica el estado actual del servicio. Los siguientes son los valores posibles y sus correspondientes descripciones.<br /><br /> 1: Detenido<br />2: Otro (Inicio pendiente)<br />3: Otro (detención pendiente)<br />4: En ejecución<br />5: Otro (continuación pendiente)<br />6: Otro (pausa pendiente)<br />7: En pausa<br /><br /> Acepta valores NULL.|  
|status_desc|**nvarchar(256)**|Describe el estado actual del servicio. Los siguientes son los valores posibles y sus correspondientes descripciones.<br /><br /> Detener: El servicio está detenido.<br />Otro (operación de inicio pendiente): El servicio está en proceso de iniciarse.<br />Otro (operación de detención pendiente): El servicio está deteniéndose.<br />Ejecutando: El servicio se está ejecutando.<br />Otros (operaciones de continuación pendientes): El servicio está en un estado pendiente.<br />Otro (pausa pendiente): El servicio está en el proceso de poner en pausa.<br />En pausa: El servicio está en pausa.<br /><br /> No puede ser null.|  
|process_id|**int**|Identificador de proceso del servicio. No puede ser null.|  
|last_startup_time|**datetimeoffset(7)**|Fecha y hora en que el servicio se inició por última vez. Acepta valores NULL.|  
|service_account|**nvarchar(256)**|Cuenta autorizada para controlar el servicio. Esta cuenta puede iniciar o detener el servicio, o puede modificar las propiedades del servicio. No puede ser null.|  
|filename|**nvarchar(256)**|Ruta de acceso y nombre del archivo ejecutable del servicio. No puede ser null.|  
|is_clustered|**nvarchar(1)**|Indica si el servicio está instalado como un recurso de un servidor en clúster. No puede ser null.|  
|cluster_nodename|**nvarchar(256)**|Nombre del nodo de clúster en el que está instalado el servicio. Acepta valores NULL.|
|instant_file_initialization_enabled|**nvarchar(1)**|Especifica si la inicialización instantánea de archivos está habilitada para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] service.<br /><br />Y = inicialización instantánea de archivos está habilitada para el servicio.<br /><br />N = inicialización instantánea de archivos está deshabilitada para el servicio.<br /><br /> Acepta valores NULL.<br /><br /> **Nota:** No se aplica a otros servicios, como el Agente SQL Server.<br /><br /> **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (A partir de [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  

## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
