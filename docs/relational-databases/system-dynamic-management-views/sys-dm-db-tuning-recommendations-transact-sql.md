---
title: sys.dm_db_tuning_recommendations (Transact-SQL) Microsoft Docs
description: Obtenga información sobre cómo encontrar posibles problemas de rendimiento y correcciones recomendadas en SQL Server y Azure SQL Database
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
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285555"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_recomendaciones de optimización\_de base de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Devuelve información detallada sobre las recomendaciones de ajuste.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, se filtran todas las filas que contienen datos que no pertenecen al inquilino conectado.

| **Nombre de la columna** | **Tipo de datos** | **Descripción** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nombre único de la recomendación. |
| **type** | **nvarchar(4000)** | El nombre de la opción de ajuste automático que produjo la recomendación, por ejemplo,`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Razón por la que se proporcionó esta recomendación. |
| **válido\_desde** | **datetime2** | La primera vez que se generó esta recomendación. |
| **última\_actualización** | **datetime2** | La última vez que se generó esta recomendación. |
| **state** | **nvarchar(4000)** | Documento JSON que describe el estado de la recomendación. Están disponibles los siguientes campos:<br />-   `currentValue`- estado actual de la recomendación.<br />-   `reason`- constante que describe por qué la recomendación está en el estado actual.|
| **es\_\_acción ejecutable** | **bit** | 1 - La recomendación se [!INCLUDE[tsql_md](../../includes/tsql-md.md)] puede ejecutar en la base de datos a través de script.<br />0 - La recomendación no se puede ejecutar en la base de datos (por ejemplo: sólo información o recomendación revertida) |
| **es\_\_acción revertida** | **bit** | 1 - El motor de base de datos puede supervisar y revertir automáticamente la recomendación.<br />0 - La recomendación no se puede supervisar y revertir automáticamente. La &quot;&quot; mayoría de &quot;las&quot;acciones ejecutables serán reviertables. |
| **ejecutar\_\_la\_hora de inicio de la acción** | **datetime2** | Fecha de aplicación de la recomendación. |
| **duración\_\_de la acción de ejecución** | **time** | Duración de la acción de ejecución. |
| **ejecutar\_\_la\_acción iniciada por** | **nvarchar(4000)** | `User`• Plan forzado por el usuario manualmente en la recomendación. <br /> `System`• El sistema aplica automáticamente la recomendación. |
| **ejecutar\_\_el\_tiempo iniciado de la acción** | **datetime2** | Fecha de aplicación de la recomendación. |
| **revertir\_\_la\_hora de inicio de la acción** | **datetime2** | Fecha en que se revirtió la recomendación. |
| **revertir\_\_la duración de la acción** | **time** | Duración de la acción de reversión. |
| **revertir\_\_la\_acción iniciada por** | **nvarchar(4000)** | `User`• Plan recomendado no forzado manualmente por el usuario. <br /> `System`• El sistema revirtió automáticamente la recomendación. |
| **revertir\_\_el\_tiempo iniciado acción** | **datetime2** | Fecha en que se revirtió la recomendación. |
| **Puntuación** | **int** | Valor/impacto estimado para esta recomendación en la escala 0-100 (cuanto mayor sea el mejor) |
| **Detalles** | **nvarchar(max)** | Documento JSON que contiene más detalles sobre la recomendación. Están disponibles los siguientes campos:<br /><br />`planForceDetails`<br />-    `queryId`-\_identificador de consulta de la consulta regresiva.<br />-    `regressedPlanId`- plan_id del plan regresivo.<br />-   `regressedPlanExecutionCount`- Número de ejecuciones de la consulta con plan regresivo antes de que se detecte la regresión.<br />-    `regressedPlanAbortedCount`- Número de errores detectados durante la ejecución del plan regresivo.<br />-    `regressedPlanCpuTimeAverage`- Tiempo medio de CPU (en micro segundos) consumido por la consulta regresiva antes de que se detecte la regresión.<br />-    `regressedPlanCpuTimeStddev`- Desviación estándar del tiempo de CPU consumido por la consulta regresiva antes de que se detecte la regresión.<br />-    `recommendedPlanId`- plan_id del plan que debe ser forzado.<br />-   `recommendedPlanExecutionCount`- Número de ejecuciones de la consulta con el plan que se deben forzar antes de que se detecte la regresión.<br />-    `recommendedPlanAbortedCount`- Número de errores detectados durante la ejecución del plan que deben ser forzados.<br />-    `recommendedPlanCpuTimeAverage`- Tiempo medio de CPU (en micro segundos) consumido por la consulta ejecutada con el plan que se debe forzar (calculado antes de que se detecte la regresión).<br />-    `recommendedPlanCpuTimeStddev`Desviación estándar del tiempo de CPU consumido por la consulta regresiva antes de que se detecte la regresión.<br /><br />`implementationDetails`<br />-  `method`- El método que se debe utilizar para corregir la regresión. El valor `TSql`es siempre .<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]script que se debe ejecutar para forzar el plan recomendado. |
  
## <a name="remarks"></a>Observaciones  
 La información `sys.dm_db_tuning_recommendations` devuelta por se actualiza cuando el motor de base de datos identifica la posible regresión del rendimiento de las consultas y no se conserva. Las recomendaciones se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantienen solo hasta que se reinicia. Los administradores de bases de datos deben realizar copias de seguridad periódicamente de la recomendación de optimización si desean conservarla después del reciclaje del servidor. 

 `currentValue`campo en `state` la columna puede tener los siguientes valores:
 
 | Status | Descripción |
 |--------|-------------|
 | `Active` | La recomendación está activa y aún no se ha aplicado. El usuario puede tomar el script de recomendación y ejecutarlo manualmente. |
 | `Verifying` | La recomendación [!INCLUDE[ssde_md](../../includes/ssde_md.md)] se aplica mediante un proceso de verificación interna que compara el rendimiento del plan forzado con el plan regresivo. |
 | `Success` | La recomendación se aplica correctamente. |
 | `Reverted` | La recomendación se revierte porque no hay mejoras significativas en el rendimiento. |
 | `Expired` | La recomendación ha expirado y ya no se puede aplicar. |

El documento `state` JSON de la columna contiene el motivo que describe por qué está la recomendación en el estado actual. Los valores en el campo de motivo pueden ser: 

| Motivo | Descripción |
|--------|-------------|
| `SchemaChanged` | La recomendación expiró porque se cambia el esquema de una tabla a la que se hace referencia. Se creará una nueva recomendación si se detecta una nueva regresión del plan de consulta en el nuevo esquema. |
| `StatisticsChanged`| La recomendación expiró debido al cambio estadístico en una tabla a la que se hace referencia. Se creará una nueva recomendación si se detecta una nueva regresión del plan de consulta basada en nuevas estadísticas. |
| `ForcingFailed` | El plan recomendado no se puede forzar en una consulta. Busque `last_force_failure_reason` en la vista [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para encontrar la razón del error. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`opción es deshabilitada por el usuario durante el proceso de verificación. Habilitar `FORCE_LAST_GOOD_PLAN` opción mediante [ALTER DATABASE SET AUTOMATIC_TUNING &#40;instrucción de&#41;de Transact-SQLTransact-SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md) o forzar el plan manualmente mediante el script en `[details]` la columna. |
| `UnsupportedStatementType` | El plan no se puede forzar en la consulta. Ejemplos de consultas no admitidas son cursores e `INSERT BULK` instrucción. |
| `LastGoodPlanForced` | La recomendación se aplica correctamente. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]se ha identificado una `FORCE_LAST_GOOD_PLAN` posible regresión de rendimiento, pero la opción no está habilitada: vea [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQLTransact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplique la recomendación `FORCE_LAST_GOOD_PLAN` manualmente o habilite la opción. |
| `VerificationAborted`| El proceso de verificación se anula debido al reinicio o a la limpieza del almacén de consultas. |
| `VerificationForcedQueryRecompile`| La consulta se vuelve a compilar porque no hay ninguna mejora significativa del rendimiento. |
| `PlanForcedByUser`| El usuario forzó manualmente el plan mediante [sp_query_store_force_plan procedimiento de&#41;de Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) &#40;. Motor de base de datos no aplicará la recomendación si el usuario decidió explícitamente forzar algún plan. |
| `PlanUnforcedByUser` | El usuario no forzó manualmente el plan mediante [sp_query_store_unforce_plan procedimiento de&#41;de Transact-SQLTransact-SQL &#40;.](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) Dado que el usuario revirtió explícitamente el plan recomendado, el motor de base de datos seguirá usando el plan actual y generará una nueva recomendación si se produce alguna regresión del plan en el futuro. |

 Las estadísticas de la columna de detalles no muestran las estadísticas del plan de tiempo de ejecución (por ejemplo, el tiempo de CPU actual). Los detalles de la recomendación se [!INCLUDE[ssde_md](../../includes/ssde_md.md)] toman en el momento de la detección de regresión y describen por qué se identificó la regresión de rendimiento. Use `regressedPlanId` `recommendedPlanId` y consulte vistas de [catálogo del Almacén](../../relational-databases/performance/how-query-store-collects-data.md) de consultas para buscar estadísticas exactas del plan en tiempo de ejecución.

## <a name="examples-of-using-tuning-recommendations-information"></a>Ejemplos de uso de la información de recomendaciones de ajuste  

### <a name="example-1"></a>Ejemplo 1
A continuación se obtiene [!INCLUDE[tsql](../../includes/tsql-md.md)] el script generado que fuerza un buen plan para cualquier consulta determinada:  
 
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
A continuación se obtiene [!INCLUDE[tsql](../../includes/tsql-md.md)] el script generado que fuerza un buen plan para cualquier consulta determinada e información adicional sobre la ganancia estimada:

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
A continuación se obtiene [!INCLUDE[tsql](../../includes/tsql-md.md)] el script generado que fuerza un buen plan para cualquier consulta determinada e información adicional que incluya el texto de consulta y los planes de consulta almacenados en el Almacén de consultas:

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

Para obtener más información acerca de las funciones JSON que se [!INCLUDE[ssde_md](../../includes/ssde_md.md)]pueden utilizar para consultar valores en la vista de recomendaciones, consulte Compatibilidad con [JSON](../../relational-databases/json/index.md) en .
  
## <a name="permissions"></a>Permisos  

Requiere `VIEW SERVER STATE` permiso [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]en .   
Requiere el `VIEW DATABASE STATE` permiso para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]la base de datos en .   

## <a name="see-also"></a>Consulte también  
 [Sintonización automática](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;&#41;de Transact-SQLTransact-SQL](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQLTransact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Compatibilidad con JSON](../../relational-databases/json/index.md)
 
