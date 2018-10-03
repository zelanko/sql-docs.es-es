---
title: Sys.dm_operation_status (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 335888ba664751bb20348472736ad697b8fe2b6d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633483"
---
# <a name="sysdmoperationstatus-azure-sql-database"></a>sys.dm_operation_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Devuelve información acerca de las operaciones realizadas en las bases de datos de un servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|Identificador de la operación. No es null.|  
|resource_type|**int**|Indica el tipo de recurso en el que se realiza la operación. No es null. En la versión actual, esta vista solo realiza el seguimiento de las operaciones realizadas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], y el valor entero correspondiente es 0.|  
|resource_type_desc|**nvarchar(2048)**|Descripción del tipo de recurso en el que se realiza la operación. En la versión actual, esta vista solo realiza el seguimiento de las operaciones realizadas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|major_resource_id|**sql_variant**|Nombre del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] en el que se realiza la operación. No NULL.|  
|minor_resource_id|**sql_variant**|Exclusivamente para uso interno. No es null.|  
|operación|**nvarchar(60)**|Operación realizada en un [!INCLUDE[ssSDS](../../includes/sssds-md.md)], como CREATE o ALTER.|  
|state|**tinyint**|El estado de la operación.<br /><br /> 0 = Pendiente<br />1 = en curso<br />2= Completado<br />3 = error<br />4 = Cancelado|  
|state_desc|**nvarchar(120)**|PENDING = la operación está esperando disponibilidad de los recursos o la cuota.<br /><br /> IN_PROGRESS = la operación se ha iniciado y está en curso.<br /><br /> COMPLETED = la operación finalizó correctamente.<br /><br /> FAILED= se produjo un error en la operación Consulte la **error_desc** columna para obtener más información.<br /><br /> CANCELLED = la operación se detuvo a petición del usuario.|  
|percent_complete|**int**|Porcentaje de la operación que se ha completado. Los valores no son continuos y los valores válidos se enumeran a continuación. No es NULL.<br/><br/>0 = no ha iniciado la operación<br/>50 = la operación en curso<br/>100 = operación completada|  
|error_code|**int**|Código que indica el error que se produjo durante una operación con errores. Si el valor es 0, indica que la operación se completó correctamente.|  
|error_desc|**nvarchar(2048)**|Descripción del error que se produjo durante una operación con errores.|  
|error_severity|**int**|Nivel de gravedad del error que se produjo durante una operación con errores. Para obtener más información sobre los niveles de gravedad de error, consulte [niveles de gravedad de Error de motor de base de datos](http://go.microsoft.com/fwlink/?LinkId=251052).|  
|error_state|**int**|Reservado para uso futuro. La compatibilidad con versiones posteriores no está garantizada.|  
|start_time|**datetime**|Marca de tiempo del inicio de la operación.|  
|last_modify_time|**datetime**|Marca de tiempo en la que se modificó el registro por última vez para una operación de ejecución prolongada. En el caso de operaciones completadas correctamente, este campo muestra la marca de tiempo en la que se completó la operación.|  
  
## <a name="permissions"></a>Permisos  
 Esta vista solo está disponible en el **maestro** base de datos para el inicio de sesión de entidad de seguridad de nivel de servidor.  
  
## <a name="remarks"></a>Comentarios  
 Para usar esta vista, debe estar conectado a la **maestro** base de datos. Use la `sys.dm_operation_status` ver en el **maestro** base de datos de la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server un seguimiento del estado de las operaciones siguientes realizadas en un [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:  
  
-   Crear base de datos  
  
-   Copiar base de datos. Copia de base de datos crea un registro en esta vista en los servidores de origen y destino.  
  
-   Modificar base de datos  
  
-   Cambiar el nivel de rendimiento de un nivel de servicio  
  
-   Cambiar el nivel de servicio de una base de datos, por ejemplo, cambiar de básico a estándar.  
  
-   Configuración de una relación de replicación geográfica  
  
-   Terminación de una relación de replicación geográfica  
  
-   Restaurar base de datos  
  
-   Eliminar base de datos  
  
## <a name="example"></a>Ejemplo  
 Mostrar las operaciones de replicación geográfica más recientes asociadas con la base de datos 'mydb'.  
  
```  
SELECT * FROM sys.dm_ operation_status   
   WHERE major_resource_id = ‘myddb’   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de replicación geográfica &#40;base de datos SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [Sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [Sys.geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
