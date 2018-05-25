---
title: Sys.dm_clr_appdomains (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e37769be6369fe1a18b8c6fb03dbecd534df502a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada dominio de aplicación en el servidor. Dominio de aplicación (**AppDomain**) es una construcción en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) que es la unidad de aislamiento para una aplicación. Puede usar esta vista para entender y solucionar problemas de objetos de integración de CLR que se ejecutan en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Existen varios tipos de objetos de base de datos administrados de integración CLR. Para obtener información general acerca de estos objetos, consulte [creación de objetos de base de datos con la integración de Common Language Runtime (CLR)](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md). Cada vez que se ejecuten estos objetos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un **AppDomain** donde puede cargar y ejecutar el código necesario. El nivel de aislamiento para una **AppDomain** es una **AppDomain** por base de datos por el propietario. Es decir, todos los objetos CLR que pertenecen a un usuario siempre se ejecutan en el mismo **AppDomain** por base de datos (si un usuario registra objetos de base de datos CLR en diferentes bases de datos, la base de datos CLR que se ejecutarán objetos en distintos dominios de aplicación). Un **AppDomain** se destruye cuando el código finaliza la ejecución. sino que se almacena en la memoria caché de cara a futuras ejecuciones. Esto mejora el rendimiento.  
  
 Para obtener más información, consulte [dominios de aplicación](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary (8)**|Dirección de la **AppDomain**. Base de datos administrado todos los objetos que pertenecen a un usuario siempre se cargan en el mismo **AppDomain**. Puede utilizar esta columna para buscar todos los ensamblados cargados actualmente en este **AppDomain** en **sys.dm_clr_loaded_assemblies**.|  
|**appdomain_id**|**int**|Id. de la **AppDomain**. Cada **AppDomain** tiene un identificador único.|  
|**appdomain_name**|**varchar(386)**|Nombre de la **AppDomain** tal como lo asignó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**creation_time**|**datetime**|Hora del **AppDomain** se creó. Dado que **AppDomains** se almacena en caché y volver a usar para mejorar el rendimiento, **creation_time** no es necesariamente el tiempo cuando se ejecuta el código.|  
|**db_id**|**int**|Id. de la base de datos en la que **AppDomain** se creó. Código almacenado en dos bases de datos no puede compartir un **AppDomain**.|  
|**USER_ID**|**int**|Id. del usuario cuyos objetos pueden ejecutarse en este **AppDomain**.|  
|**state**|**nvarchar(128)**|Un descriptor para el estado actual de la **AppDomain**. Un AppDomain puede encontrarse en estados diferentes desde la creación a la eliminación. Vea la sección Comentarios de este tema para obtener más información.|  
|**strong_refcount**|**int**|Número de referencias seguras a este **AppDomain**. Esto refleja el número de lotes en ejecución que utilicen esta **AppDomain**. Tenga en cuenta que la ejecución de esta vista creará un **recuento de referencias seguro**; incluso si hay código que se está ejecutando actualmente, **strong_refcount** tendrá un valor de 1.|  
|**weak_refcount**|**int**|Número de referencias débiles a este **AppDomain**. Esto indica cuántos objetos dentro de la **AppDomain** se almacenan en caché. Cuando se ejecuta un objeto de base de datos administrados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo almacena en caché dentro de la **AppDomain** para reutilizarlo en un futuro. Esto mejora el rendimiento.|  
|**Costo**|**int**|Costo de la **AppDomain**. Cuanto mayor sea el costo, más probable que esto **AppDomain** se descargue bajo presión de memoria. Costo suele depende de la cantidad de memoria es necesario para volver a crear esta **AppDomain**.|  
|**value**|**int**|Valor de la **AppDomain**. Cuanto menor sea el valor, más probable que esto **AppDomain** se descargue bajo presión de memoria. Valor suele depende de cuántas conexiones o lotes que estén usando este **AppDomain**.|  
|**total_processor_time_ms**|**bigint**|Tiempo total del procesador, en milisegundos, consumido por todos los subprocesos durante la ejecución en el dominio de aplicación actual desde que se inició el proceso. Esto equivale a **System.AppDomain.MonitoringTotalProcessorTime**.|  
|**total_allocated_memory_kb**|**bigint**|Tamaño total, en kilobytes, de todas las asignaciones de memoria realizadas por el dominio de aplicación desde que se creó, sin restar memoria recopilada. Esto equivale a **System.AppDomain.MonitoringTotalAllocatedMemorySize**.|  
|**survived_memory_kb**|**bigint**|Número de kilobytes que sobrevivieron a la última colección de bloqueo completa a que debe hacer referencia el dominio de aplicación actual. Esto equivale a **System.AppDomain.MonitoringSurvivedMemorySize**.|  
  
## <a name="remarks"></a>Comentarios  
 Hay una relación de uno a mayo entre **dm_clr_appdomains.appdomain_address** y **dm_clr_loaded_assemblies.appdomain_address**.  
  
 Las tablas siguientes se muestran los posibles **estado** valores, sus descripciones y cuándo se producen en el **AppDomain** ciclo de vida. Puede usar esta información para seguir el ciclo de vida de un **AppDomain** y para inspeccionar los sospechosas o repetitivas **AppDomain** instancias descargar, sin tener que analizar el registro de eventos de Windows.  
  
## <a name="appdomain-initialization"></a>Inicialización de AppDomain  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|El **AppDomain** se está creando.|  
  
## <a name="appdomain-usage"></a>Uso de AppDomain  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|El tiempo de ejecución **AppDomain** está listo para su uso por varios usuarios.|  
|E_APPDOMAIN_SINGLEUSER|El **AppDomain** está listo para su uso en operaciones de DDL. Se diferencian de E_APPDOMAIN_SHARED en que AppDomains compartidos se usan para ejecuciones de integración CLR en contraposición con operaciones de DDL. Dichos AppDomains están aislados de las operaciones simultáneas.|  
|E_APPDOMAIN_DOOMED|El **AppDomain** está programado que se descarga, pero actualmente no hay subprocesos que se ejecutan en él.|  
  
## <a name="appdomain-cleanup"></a>Limpieza de AppDomain  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha solicitado que CLR descargue el **AppDomain**, normalmente porque se ha modificado o quitado el ensamblado que contiene los objetos de base de datos administrados.|  
|E_APPDOMAIN_UNLOADED|CLR ha descargado la **AppDomain**. Esto suele ser el resultado de un procedimiento de concentración debido a **ThreadAbort**, **OutOfMemory**, o una excepción no controlada en el código de usuario.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|El **AppDomain** se ha descargado en CLR y establezca que destruya [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_DESTROY|El **AppDomain** está destruyendo por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_ZOMBIE|El **AppDomain** ha destruido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; sin embargo, no todas las referencias a la **AppDomain** se han limpiado.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo ver los detalles de un **AppDomain** para un determinado ensamblado:  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 En el ejemplo siguiente se muestra cómo ver todos los ensamblados en un determinado **AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Vistas de administración dinámica relacionadas con el Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
