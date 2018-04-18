---
title: sysdac_history_internal (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a6c3f5690f60fb1343df27db377af42938da805
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>Tablas de aplicación de capa de datos - sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre las acciones realizadas para administrar las aplicaciones de capa de datos (DAC). Esta tabla se almacena en la **dbo** esquema de la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|Identificador de la acción|  
|**sequence_id**|**int**|Identifica un paso dentro de una acción.|  
|**valor de instance_id**|**uniqueidentifier**|Identificador de la instancia de DAC. Esta columna se puede combinar en el **instance_id** columna en [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md).|  
|**action_type**|**tinyint**|Identificador del tipo de acción:<br /><br /> **0** = implementar<br /><br /> **1** = crear<br /><br /> **2** = cambio de nombre<br /><br /> **3** = separar<br /><br /> **4** = eliminar|  
|**action_type_name**|**varchar (19)**|Nombre del tipo de acción:<br /><br /> **Implementar**<br /><br /> **Crear**<br /><br /> **Cambiar el nombre**<br /><br /> **detach**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|Identificador del tipo de objeto afectado por la acción:<br /><br /> **0** = dacpac<br /><br /> **1** = inicio de sesión<br /><br /> **2** = base de datos|  
|**dac_object_type_name**|**varchar (8)**|Nombre del tipo de objeto afectado por la acción:<br /><br /> **dacpac** = instancia de DAC<br /><br /> **Inicio de sesión**<br /><br /> **database**|  
|**action_status**|**tinyint**|Código que identifica el estado actual de la acción:<br /><br /> **0** = pendiente<br /><br /> **1** = correcto<br /><br /> **2** = error|  
|**action_status_name**|**varchar (11)**|Estado actual de la acción:<br /><br /> **Pendiente**<br /><br /> **Correcto**<br /><br /> **Un error**|  
|**Necesario**|**bit**|Lo utiliza el [!INCLUDE[ssDE](../../includes/ssde-md.md)] al revertir una operación DAC.|  
|**dac_object_name_pretran**|**sysname**|Nombre del objeto antes de que se confirme la transacción que contiene la acción. Solo se utiliza para las bases de datos e inicios de sesión.|  
|**dac_object_name_posttran**|**sysname**|Nombre del objeto después de que se confirme la transacción que contiene la acción. Solo se utiliza para las bases de datos e inicios de sesión.|  
|**en SqlScript**|**nvarchar(max)**|Script [!INCLUDE[tsql](../../includes/tsql-md.md)] que implementa una acción en una base de datos o inicio de sesión.|  
|**carga**|**varbinary(max)**|Definición de paquete DAC guardada en una cadena con codificación binaria.|  
|**Comentarios**|**ntext**|Registra el inicio de sesión de un usuario que ha aceptado una pérdida de datos potencial en una actualización de DAC.|  
|**error_string**|**nvarchar(max)**|Mensaje de error generado si la acción encuentra un error.|  
|**created_by**|**sysname**|Inicio de sesión que inició la acción que creó esta entrada.|  
|**date_created**|**datetime**|Fecha y hora en que se creó esta entrada.|  
|**date_modified**|**datetime**|Fecha y hora en la que se modificó por última vez la entrada.|  
  
## <a name="remarks"></a>Comentarios  
 Las acciones de administración de una DAC, por ejemplo su implementación o eliminación, generan varios pasos. A cada acción se le asigna un identificador de acción. Cada paso se le asigna un número de secuencia y una fila de **sysdac_history_internal**, donde se graba el estado del paso. Cada fila se crea cuando el paso de la acción comienza y se actualiza según convenga para reflejar el estado de la operación. Por ejemplo, se podría asignar una acción de DAC implementar **action_id** 12 y puede obtener cuatro filas en **sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|crear|dacpac|  
|12|1|crear|login|  
|12|2|crear|database|  
|12|3|cambiar el nombre|database|  
  
 Operaciones de DAC, como la eliminación, no quitan filas de **sysdac_history_internal**. Puede usar la siguiente consulta para eliminar manualmente las filas de las DAC que ya no se implementen en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 Si se eliminan filas de DAC activas, no influyen en las operaciones DAC; lo único que ocurre es que no podrá informar del historial completo de la DAC.  
  
> [!NOTE]  
>  Actualmente, no hay ningún mecanismo para eliminar **sysdac_history_internal** filas en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor sysadmin. Acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la base de datos maestra.  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
