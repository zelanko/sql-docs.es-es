---
title: sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176256"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Devuelve la configuración del gobierno de recursos y la configuración de capacidad de una base de datos Azure SQL Database.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|int|IDENTIFICADOR de la base de datos, único dentro de un servidor de Azure SQL Database.|
|**logical_database_guid**|uniqueidentifier|GUID lógico para la base de datos de usuario y permanece a lo largo de la vida de una base de datos de usuario.  Cambiar el nombre o establecer una base de datos en un SLO diferente no cambiará el GUID. |
|**physical_database_guid**|uniqueidentifier|GUID físico para una base de datos de usuario que permanece a lo largo de la vida de la instancia física de la base de datos de usuario. Establecer en un SLO diferente hará que esta columna cambie.|
|**server_name**|nvarchar|Nombre del servidor lógico.|
|**database_name**|nvarchar|Nombre de la base de datos lógica.|
|**slo_name**|nvarchar|Generación de hardware y objetivo de nivel de servicio.|
|**dtu_limit**|int|Límite de DTU de la base de datos (NULL para núcleo virtual).|
|**cpu_limit**|int|Núcleo virtual límite de base de datos (NULL para las bases de datos de DTU).|
|**min_cpu**|tinyint|Porcentaje mínimo de CPU que puede usar la carga de trabajo del usuario.|
|**max_cpu**|tinyint|Porcentaje máximo de CPU que puede usar la carga de trabajo del usuario.|
|**cap_cpu**|tinyint|Límite de porcentaje de CPU para grupos de cargas de trabajo de usuario.|
|**min_cores**|smallint|Número de CPU usadas por SQL.|
|**max_dop**|smallint|Grado máximo de paralelismo usado por la carga de trabajo del usuario.|
|**min_memory**|int|Porcentaje mínimo de memoria que puede usar la carga de trabajo del usuario.|
|**max_memory**|int|Porcentaje máximo de memoria que puede usar la carga de trabajo del usuario.|
|**max_sessions**|int|Límite de sesión para el grupo de usuarios.|
|**max_memory_grant**|int|Concesión de memoria máxima para cada consulta en la carga de trabajo de usuario, en porcentaje.|
|**max_db_memory**|int|Límite máximo de memoria del grupo de búferes para la carga de trabajo de base de usuarios|
|**govern_background_io**|bit|Indica si se cargan las operaciones de escritura en segundo plano en el grupo de usuarios.|
|**min_db_max_size_in_mb**|bigint|Tamaño mínimo máximo del archivo de base de datos, en MB.|
|**max_db_max_size_in_mb**|bigint|Máximo de archivo de base de datos, en MB.|
|**default_db_max_size_in_mb**|bigint|Tamaño máximo predeterminado del archivo de base de datos, en MB.|
|**db_file_growth_in_mb**|bigint|Crecimiento predeterminado del archivo de base de datos de Azure, en MB.|
|**initial_db_file_size_in_mb**|bigint|Tamaño predeterminado del archivo de base de datos, en MB.|
|**log_size_in_mb**|bigint|Tamaño predeterminado del archivo de registro, en MB.|
|**instance_cap_cpu**|int|Límite de CPU en el nivel de instancia.|
|**instance_max_log_rate**|bigint|Límite de velocidad de generación de registros en el nivel de instancia, en bytes por segundo.|
|**instance_max_worker_threads**|int|Límite de subprocesos de trabajo en el nivel de instancia.|
|**replica_type**|int|Tipo de réplica, donde 0 es principal y 1 es secundario.|
|**max_transaction_size**|bigint|Espacio de registro máximo usado por cualquier transacción, en KB.|
|**checkpoint_rate_mbps**|int|Ancho de banda de punto de comprobación, en Mbps.|
|**checkpoint_rate_io**|int|Tasa de e/s de punto de comprobación en IOs por segundo.|
|**last_updated_date_utc**|datetime|Fecha y hora del último cambio o reconfiguración de la configuración.|
|**primary_group_id**|int|IDENTIFICADOR del grupo de cargas de trabajo del usuario primario.|
|**primary_group_max_workers**|int|Límite de trabajo en el nivel de grupo de cargas de trabajo de usuario primario.|
|**primary_min_log_rate**|bigint|Velocidad de registro mínima (bytes por segundo) en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_max_log_rate**|bigint|Velocidad de registro máxima (bytes por segundo) en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_group_min_io**|int|Mínimo de e/s en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_group_max_io**|int|Máximo de e/s en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_group_min_cpu**|float|Límite mínimo de porcentaje de CPU en el nivel de grupo de cargas de trabajo de usuario primario.|
|**primary_group_max_cpu**|float|Límite máximo de porcentaje de CPU en el nivel de grupo de cargas de trabajo de usuario primario.|
|**primary_log_commit_fee**|int|Cuota de confirmación del gobierno de velocidad de registro en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_pool_max_workers**|int|Límite de trabajo en el nivel de grupo de usuarios principal.
|**pool_max_io**|int|Límite máximo de e/s en el nivel de grupo de usuarios principal.|
|**govern_db_memory_in_resource_pool**|bit|Indica si el tamaño máximo del grupo de búferes se rige en el nivel de grupo de recursos. Normalmente se establece para las bases de datos de grupos elásticos.|
|**volume_local_iops**|int|Límite de e/s por segundo para el volumen local (por ejemplo, C:, D:).|
|**volume_managed_xstore_iops**|int|Cap de IOs por segundo para la cuenta de almacenamiento remoto.|
|**volume_external_xstore_iops**|int|Cap de IOs por segundo para la cuenta de almacenamiento remoto que usan las copias de seguridad y la telemetría de Azure SQL DB.|
|**volume_type_local_iops**|int|Cap de IOs por segundo para todos los volúmenes locales.|
|**volume_type_managed_xstore_iops**|int|Cap de IOs por segundo para todas las cuentas de almacenamiento remoto utilizadas por la instancia.|
|**volume_type_external_xstore_iops**|int|Cap de IOs por segundo para todas las cuentas de almacenamiento remoto usadas por las copias de seguridad de Azure SQL DB y la telemetría de la instancia.|
|**volume_pfs_iops**|int|Cap de IOs por segundo para el almacenamiento de archivos Premium.|
|**volume_type_pfs_iops**|int|Cap de IOs por segundo para todo el almacenamiento de archivos Premium usado por la instancia de.|
|||

## <a name="permissions"></a>Permisos

Esta vista necesita el permiso VIEW DATABASE STATE.

## <a name="remarks"></a>Comentarios

Los usuarios pueden tener acceso a esta vista de administración dinámica para la configuración de gobierno de recursos y la configuración de capacidad de una base de datos Azure SQL Database. 

> [!IMPORTANT]
> La mayoría de los datos expuestos por esta DMV están destinados al consumo interno y están sujetos a cambios.

## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se devuelven datos de velocidad de registro máxima de instancia ordenados por nombre de base de datos en el servidor de base de datos para una base de datos única o agrupada.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Vea también

- [Gobierno de velocidad de registro de transacciones](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Límites de recursos de DTU de una sola base de datos](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Límites de recursos núcleo virtual de base de datos única](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
