---
title: sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: bb4c43fa4193d9254d7f06f24bd903f974739e87
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567641"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Devuelve valores de configuración y la capacidad para una base de datos de Azure SQL Database de regulación de recursos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|INT|Id. de la base de datos, único dentro de un servidor de base de datos de SQL Azure.|
|**logical_database_guid**|UNIQUEIDENTIFIER|Guid lógico de base de datos de usuario y permanece a través de la vida de una base de datos de usuario.  Cambiar el nombre o establecer una base de datos en otro SLO no cambiará el GUID. |
|**physical_database_guid**|UNIQUEIDENTIFIER|Guid de física de una base de datos de usuario que permanece a través de la vida de la instancia física de la base de datos de usuario. Configuración para un SLO diferentes hará que esta columna para cambiar.|
|**server_name**|NVARCHAR|Nombre del servidor lógico.|
|**database_name**|NVARCHAR|Nombre de la base de datos lógica.|
|**slo_name**|NVARCHAR|Servicio objetivo generación y nivel de hardware.|
|**dtu_limit**|INT|Límite de DTU de la base de datos (es NULL para memoria con núcleo virtual).|
|**cpu_limit**|INT|límite de memoria con núcleo virtual de base de datos (es NULL para las bases de datos DTU).|
|**min_cpu**|TINYINT|Porcentaje de CPU mínimo que puede usarse por carga de trabajo de usuario.|
|**max_cpu**|TINYINT|Porcentaje máximo de CPU que puede usarse por carga de trabajo de usuario.|
|**cap_cpu**|TINYINT|Límite de porcentaje de CPU para grupos de cargas de trabajo de usuarios.|
|**min_cores**|SMALLINT|Número de CPU utilizado por SQL.|
|**max_dop**|SMALLINT|Grado máximo de paralelismo que se usa por carga de trabajo de usuario.|
|**min_memory**|INT|Porcentaje de memoria mínima que puede usarse por carga de trabajo de usuario.|
|**max_memory**|INT|Porcentaje de memoria máxima que puede usarse por carga de trabajo de usuario.|
|**max_sessions**|INT|Límite de sesión para el grupo de usuarios.|
|**max_memory_grant**|INT|Concesión de memoria máximo para cada consulta de carga de trabajo de usuario, en porcentaje.|
|**max_db_memory**|INT|Límite de memoria de grupo de búfer de Max para la carga de trabajo de base de datos de usuario|
|**govern_background_io**|bit|Indica si las operaciones de escritura en segundo plano se cobran al grupo de usuarios.|
|**min_db_max_size_in_mb**|BIGINT|Tamaño de archivo de base de datos Max mínima, en MB.|
|**max_db_max_size_in_mb**|BIGINT|Máximo Max base de datos de archivo, en MB.|
|**default_db_max_size_in_mb**|BIGINT|Tamaño máximo de archivo base de datos, en MB de forma predeterminada.|
|**db_file_growth_in_mb**|BIGINT|De forma predeterminada el crecimiento del archivo de base de datos de azure, en MB.|
|**initial_db_file_size_in_mb**|BIGINT|Tamaño de archivo de base de datos de la predeterminada en MB.|
|**log_size_in_mb**|BIGINT|Tamaño de archivo de registro de la predeterminada en MB.|
|**instance_cap_cpu**|INT|Límite de CPU en el nivel de instancia.|
|**instance_max_log_rate**|BIGINT|Generación de registros de límite de velocidad en el nivel de instancia, en bytes por segundo.|
|**instance_max_worker_threads**|INT|Límite de subprocesos de trabajo en el nivel de instancia.|
|**replica_type**|INT|Tipo de réplica, donde 0 es el principal y 1 es secundaria.|
|**max_transaction_size**|BIGINT|Espacio de registro máximo utilizado por cualquier transacción, en KB.|
|**checkpoint_rate_mbps**|INT|Ancho de banda de punto de control, en Mbps.|
|**checkpoint_rate_io**|INT|Tasa de E/S de punto de comprobación en IOs por segundo.|
|**last_updated_date_utc**|DATETIME|Fecha y hora del último cambio de configuración o reconfiguración.|
|**primary_group_id**|INT|Id. de grupo de cargas de trabajo de usuario principal.|
|**primary_group_max_workers**|INT|Límite de trabajadores en nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_min_log_rate**|BIGINT|Tasa de registro mínimo (bytes por segundo) en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_max_log_rate**|BIGINT|Tasa de registro máximo (bytes por segundo) a nivel de grupo de cargas de trabajo principal de usuario.|
|**primary_group_min_io**|INT|Mínimo de E/S en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_group_max_io**|INT|E/S máxima en nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_group_min_cpu**|FLOAT|Porcentaje de CPU mínimo limita a nivel de grupo de cargas de trabajo principal de usuario.|
|**primary_group_max_cpu**|FLOAT|Limita el porcentaje máximo de CPU en el nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_log_commit_fee**|INT|Precio de confirmación de registro tasa gobierno en nivel de grupo de cargas de trabajo de usuario principal.|
|**primary_pool_max_workers**|INT|Límite de trabajadores a nivel de grupo principal del usuario.
|**pool_max_io**|INT|Límite máximo de E/S en el nivel del grupo principal del usuario.|
|**govern_db_memory_in_resource_pool**|bit|Indica si el tamaño máximo del grupo de búferes se rige en el nivel de grupo de recursos. Normalmente se establece para las bases de datos dentro de los grupos elásticos.|
|**volume_local_iops**|INT|E/s por segundo límite en cuanto al volumen local (por ejemplo, C:, D:).|
|**volume_managed_xstore_iops**|INT|E/s por segundo extremo para la cuenta de almacenamiento remoto.|
|**volume_external_xstore_iops**|INT|E/s por segundo extremo para la cuenta de almacenamiento remoto usada datos de telemetría y las copias de seguridad de base de datos de SQL Azure.|
|**volume_type_local_iops**|INT|E/s por segundo extremo para todos los volúmenes locales.|
|**volume_type_managed_xstore_iops**|INT|E/s por segundo extremo para todas las cuentas de almacenamiento remoto que usa la instancia.|
|**volume_type_external_xstore_iops**|INT|E/s por segundo extremo para todas las cuentas de almacenamiento remoto utilizado por las copias de seguridad de base de datos de SQL Azure y la telemetría para la instancia.|
|**volume_pfs_iops**|INT|E/s por segundo extremo para premium storage del archivo.|
|**volume_type_pfs_iops**|INT|E/s por segundo extremo para todo el almacenamiento de archivo premium usado por la instancia.|
|||

## <a name="permissions"></a>Permisos

Esta vista necesita el permiso VIEW DATABASE STATE.

## <a name="remarks"></a>Comentarios

Los usuarios pueden acceder a esta vista de administración dinámica para la configuración del gobierno de recursos y configuración de capacidad de una base de datos de Azure SQL Database. 

> [!IMPORTANT]
> La mayoría de los datos que se exponen a través de esta DMV está pensado para su uso interno y está sujeta a cambios.

## <a name="examples"></a>Ejemplos

El ejemplo siguiente devuelve la instancia máxima velocidad datos del registro ordenadas por nombre de la base de datos en el servidor de base de datos para una base de datos única o agrupada.

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>Vea también

- [Gobierno de tasa de registro de transacciones](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Límites de recursos DTU de base de datos única](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Límites de recursos de memoria con núcleo virtual de base de datos única](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
