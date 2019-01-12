---
title: Sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Obtenga información sobre cómo detectar posibles problemas de rendimiento y recomienda correcciones en SQL Server y Azure SQL Database
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21756cadbfb924e95edd261942f018fb6aef6a4c
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226522"
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>Sys.DM\_db\_optimización\_recomendaciones (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Devuelve información detallada sobre las recomendaciones de optimización.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.

| **Nombre de columna** | **Data type** | **Descripción** |
| --- | --- | --- |
| **Nombre** | **nvarchar(4000)** | Nombre único de la recomendación. |
| **Tipo** | **nvarchar(4000)** | El nombre de la opción de ajuste automático que generó la recomendación, por ejemplo, `FORCE_LAST_GOOD_PLAN` |
| **motivo** | **nvarchar(4000)** | Motivo de por qué se ha proporcionado esta recomendación. |
| **válido\_puesto que** | **datetime2** | La primera vez que se generó esta recomendación. |
| **última\_actualizar** | **datetime2** | La última vez que se generó esta recomendación. |
| **state** | **nvarchar(4000)** | Documento JSON que describe el estado de la recomendación. Están disponibles los campos siguientes:<br />-   `currentValue` -estado actual de la recomendación.<br />-   `reason` -constante que describe por qué es la recomendación en el estado actual.|
| **es\_ejecutable\_acción** | **bit** | 1 = la recomendación se puede ejecutar en la base de datos a través de [!INCLUDE[tsql_md](../../includes/tsql-md.md)] secuencia de comandos.<br />0 = no se puede ejecutar la recomendación en la base de datos (por ejemplo: recomendación de información única o revertido) |
| **es\_revertable\_acción** | **bit** | 1 = la recomendación puede supervisarse y revertir el motor de base de datos automáticamente.<br />0 = no puede ser supervisada y revierte automáticamente la recomendación. La mayoría &quot;ejecutable&quot; acciones serán &quot;revertable&quot;. |
| **ejecutar\_acción\_iniciar\_tiempo** | **datetime2** | Fecha en que se aplica la recomendación. |
| **ejecutar\_acción\_duración** | **time** | Duración de la acción de ejecución. |
| **ejecutar\_acción\_inició\_por** | **nvarchar(4000)** | `User` = Usuario forzar manualmente el plan en la recomendación. <br /> `System` = El sistema aplica automáticamente la recomendación. |
| **ejecutar\_acción\_inició\_tiempo** | **datetime2** | Fecha en que se ha aplicado la recomendación. |
| **revertir\_acción\_iniciar\_tiempo** | **datetime2** | Fecha de que la recomendación se revirtió. |
| **revertir\_acción\_duración** | **time** | Duración de la acción de reversión. |
| **revertir\_acción\_inició\_por** | **nvarchar(4000)** | `User` = Plan recomendado de usuario forzado manualmente. <br /> `System` = Sistema revierte automáticamente la recomendación. |
| **revertir\_acción\_inició\_tiempo** | **datetime2** | Fecha de que la recomendación se revirtió. |
| **puntuación** | **int** | Calcula el impacto o valor de esta recomendación en el valor de 0 a 100 escala (cuanto mayor sea la mejor) |
| **Detalles** | **nvarchar(max)** | Documento JSON que contiene información más detallada acerca de la recomendación. Están disponibles los campos siguientes:<br /><br />`planForceDetails`<br />-    `queryId` -consulta\_Id. de la consulta devuelta.<br />-    `regressedPlanId` -plan_id del plan con regresión.<br />-   `regressedPlanExecutionCount` -El número de ejecuciones de la consulta con un plan con regresión antes de la regresión se detecta.<br />-    `regressedPlanAbortedCount` -El número de errores detectados durante la ejecución del plan con regresión.<br />-    `regressedPlanCpuTimeAverage` -Promedio de tiempo de CPU utilizado por la consulta con regresión antes de que se detecta la regresión.<br />-    `regressedPlanCpuTimeStddev` : Se ha detectado desviación estándar de tiempo de CPU utilizado por las consultas con regresión antes de la regresión.<br />-    `recommendedPlanId` -plan_id del plan que se debería forzar.<br />-   `recommendedPlanExecutionCount`-El número de ejecuciones de la consulta con el plan que se debería forzar antes de que se detecta la regresión.<br />-    `recommendedPlanAbortedCount` -El número de errores detectados durante la ejecución del plan que se debería forzar.<br />-    `recommendedPlanCpuTimeAverage` -Promedio de tiempo de CPU consumido por la consulta ejecutada con el plan que se debería forzar (calculado antes de que se detecta la regresión).<br />-    `recommendedPlanCpuTimeStddev` Se ha detectado la desviación estándar de tiempo de CPU utilizado por las consultas con regresión antes de la regresión.<br /><br />`implementationDetails`<br />-  `method` -El método que se debe usar para corregir la regresión. Valor siempre es `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] secuencia de comandos que se debe ejecutar para forzar el plan recomendado. |
  
## <a name="remarks"></a>Comentarios  
 Información devuelta por `sys.dm_db_tuning_recommendations` se actualiza cuando el motor de base de datos identifica posibles regresión del rendimiento de consulta y no se conserva. Las recomendaciones se mantienen hasta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia. Los administradores de base de datos deben realizar periódicamente copias de seguridad de la recomendación de optimización si desean conservarla después de reciclar el servidor. 

 `currentValue` campo en el `state` columna puede tener los siguientes valores:
 
 | Estado | Descripción |
 |--------|-------------|
 | `Active` | Recomendación está activa y no ha aplicado. Usuario puede tomar el script de recomendación y ejecutarlo manualmente. |
 | `Verifying` | La recomendación se aplicó por [!INCLUDE[ssde_md](../../includes/ssde_md.md)] y proceso de comprobación internos compara el rendimiento del plan forzado con el plan con regresión. |
 | `Success` | La recomendación se aplicó correctamente. |
 | `Reverted` | Recomendación se revirtió porque no hay ningún aumento significativo del rendimiento. |
 | `Expired` | Recomendación ha expirado y ya no puede aplicarse. |

Documento JSON en `state` columna contiene la razón que describe por qué es la recomendación en el estado actual. Los valores del campo motivo podrían ser: 

| Reason | Descripción |
|--------|-------------|
| `SchemaChanged` | Recomendación ha caducado porque se cambia el esquema de una tabla que se hace referencia. |
| `StatisticsChanged`| Recomendación caducado debido al cambio de estadísticas en una tabla que se hace referencia. |
| `ForcingFailed` | No se puede forzar plan recomendado en una consulta. Buscar el `last_force_failure_reason` en el [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) vista para averiguar el motivo del error. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` opción está deshabilitada por el usuario durante el proceso de comprobación. Habilitar `FORCE_LAST_GOOD_PLAN` mediante la opción [ALTER DATABASE establece AUTOMATIC_TUNING &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) instrucción o forzar el plan manualmente mediante la secuencia de comandos en `[details]` columna. |
| `UnsupportedStatementType` | No se puede forzar el plan en la consulta. Ejemplos de consultas no admitidos son los cursores y `INSERT BULK` instrucción. |
| `LastGoodPlanForced` | La recomendación se aplicó correctamente. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identifica la regresión del rendimiento potencial, pero la `FORCE_LAST_GOOD_PLAN` opción no está habilitada, consulte [ALTER DATABASE establece AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplicar recomendación de forma manual o habilitar `FORCE_LAST_GOOD_PLAN` opción. |
| `VerificationAborted`| Proceso de comprobación se ha anulado debido al reinicio o limpieza de la consulta Store. |
| `VerificationForcedQueryRecompile`| Se recompila la consulta porque no hay ninguna mejora significativa del rendimiento. |
| `PlanForcedByUser`| Usuario manualmente el plan de uso forzados [sp_query_store_force_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) procedimiento. |
| `PlanUnforcedByUser` | Usuario no forzarse manualmente el plan mediante [sp_query_store_unforce_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) procedimiento. |

 Estadística de la columna de detalles no se muestran estadísticas de plan en tiempo de ejecución (por ejemplo, tiempo de CPU actual). Los detalles de recomendación se realizan en el momento de la detección de regresión y describa por qué [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regresión del rendimiento. Use `regressedPlanId` y `recommendedPlanId` a consulta [vistas de catálogo de la consulta Store](../../relational-databases/performance/how-query-store-collects-data.md) para buscar las estadísticas del plan de exacto en tiempo de ejecución.

## <a name="examples-of-using-tuning-recommendations-information"></a>Ejemplos del uso de información de las recomendaciones de optimización  

### <a name="example-1"></a>Ejemplo 1
Obtiene el texto generado lo siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] script que fuerza un buen plan para una consulta concreta:  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>Ejemplo 2
Obtiene el texto generado lo siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] script que fuerza un buen plan para cualquier consulta dada e información adicional sobre el aumento estimado:

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

### <a name="example-3"></a>Ejemplo 3
Obtiene el texto generado lo siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] script que fuerza un buen plan para cualquier consulta determinada y la información adicional que incluye el texto de consulta y los planes de consulta almacenados en la consulta Store:

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

Para obtener más información acerca de las funciones JSON que puede usarse para consultar los valores en la vista de recomendación, consulte [compatibilidad de JSON](../../relational-databases/json/index.md) en [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Permisos  

Requiere `VIEW SERVER STATE` permiso en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Requiere el `VIEW DATABASE STATE` permiso para la base de datos en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   

## <a name="see-also"></a>Vea también  
 [El ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Compatibilidad de JSON](../../relational-databases/json/index.md)
 
