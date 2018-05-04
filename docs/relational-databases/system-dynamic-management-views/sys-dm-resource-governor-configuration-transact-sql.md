---
title: Sys.dm_resource_governor_configuration (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_resource_governor_configuration_TSQL
- dm_resource_governor_configuration
- sys.dm_resource_governor_configuration
- sys.dm_resource_governor_configuration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_configuration dynamic management view
ms.assetid: c89aab6a-0434-4ce6-af8c-f8a1a3284e38
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 552b1ecbfd01afddf8671c05dcdf528f3edccb6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmresourcegovernorconfiguration-transact-sql"></a>sys.dm_resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila que contiene el estado actual de la configuración en memoria del regulador de recursos.  
  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|El Id. de la función clasificadora usada actualmente por el regulador de recursos. Devuelve el valor 0 si no se utiliza ninguna función. No admite valores NULL.<br /><br /> **Nota:** esta función se utiliza para clasificar nuevas solicitudes y usa reglas para enrutar estas solicitudes al grupo de cargas de trabajo adecuado. Para obtener más información, vea [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).|  
|is_reconfiguration_pending|**bit**|Indica si los cambios a un grupo o fondo se realizaron con la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE pero no se han aplicado a la configuración en memoria. El valor devuelto puede ser:<br /><br /> 0 = No es necesaria una instrucción de reconfiguración.<br /><br /> 1 = Es necesaria una instrucción de reconfiguración o un reinicio del servidor para aplicar los cambios de la configuración pendientes.<br /><br /> **Nota:** el valor devuelto es siempre 0 cuando se deshabilita el regulador de recursos.<br /><br /> No admite valores NULL.|  
|max_outstanding_io_per_volume|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número máximo de operaciones de E/S pendientes por volumen.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista de administración dinámica muestra la configuración en memoria. Utilice la vista de catálogo correspondiente para ver los metadatos almacenados de la configuración.  
  
 En el siguiente ejemplo se muestra cómo obtener y comparar los valores de metadatos almacenados y los valores en memoria de la configuración del regulador de recursos.  
  
```  
USE master;  
go  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
go  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
go  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)  
  
  

