---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: "Obtenga información acerca de cómo buscar posibles problemas de rendimiento y recomienda correcciones en SQL Server y base de datos de SQL Azure"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43acc4c2bfbcb9458f93f2ad89414e3781a7836d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>Sys.DM\_db\_para la optimización\_recomendaciones (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Devuelve información detallada sobre recomendaciones de optimización.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.

| **Nombre de columna** | **Tipo de datos** | **Description** |
| --- | --- | --- |
| **Nombre** | **nvarchar(4000)** | Nombre único de la recomendación. |
| **Tipo** | **nvarchar(4000)** | El nombre de la opción de optimización automática que genera la recomendación, por ejemplo,`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Motivo por qué se proporcionó esta recomendación. |
| **valid\_since** | **datetime2** | La primera vez que se generó esta recomendación. |
| **last\_refresh** | **datetime2** | La última vez que se generó esta recomendación. |
| **state** | **nvarchar(4000)** | Documento JSON que describe el estado de la recomendación. Están disponibles los campos siguientes:<br />-   `currentValue`-estado actual de la recomendación.<br />-   `reason`– constante que describe por qué es la recomendación en el estado actual.|
| **is\_executable\_action** | **bit** | 1 = la recomendación se pueden ejecutar en la base de datos a través de [!INCLUDE[tsql_md](../../includes/tsql_md.md)] secuencia de comandos.<br />0 = la recomendación no se puede ejecutar en la base de datos (por ejemplo: recomendación solo o revertida de información) |
| **es\_revertable\_acción** | **bit** | 1 = la recomendación puede supervisarse y revertir el motor de base de datos automáticamente.<br />0 = no se puede supervisar y revierte automáticamente la recomendación. La mayoría &quot;ejecutable&quot; acciones serán &quot;revertable&quot;. |
| **execute\_action\_start\_time** | **datetime2** | Fecha en que se aplica la recomendación. |
| **execute\_action\_duration** | **time** | Duración de la acción de ejecución. |
| **execute\_action\_initiated\_by** | **nvarchar(4000)** | `User`= Usuario manualmente forzar plan en la recomendación. <br /> `System`= Sistema aplica automáticamente la recomendación. |
| **execute\_action\_initiated\_time** | **datetime2** | Fecha en que se aplicó la recomendación. |
| **revert\_action\_start\_time** | **datetime2** | Fecha en que se revirtió la recomendación. |
| **revert\_action\_duration** | **time** | Duración de la acción de reversión. |
| **revertir\_acción\_inició\_por** | **nvarchar(4000)** | `User`= Plan recomendada manualmente unforced usuario. <br /> `System`= Sistema revierte automáticamente la recomendación. |
| **revert\_action\_initiated\_time** | **datetime2** | Fecha en que se revirtió la recomendación. |
| **score** | **int** | Calcula el valor e impacto de esta recomendación en 0 y 100 escala (cuanto mayor sea la mejor) |
| **details** | **nvarchar(max)** | Documento JSON que contiene información más detallada acerca de la recomendación. Están disponibles los campos siguientes:<br /><br />`planForceDetails`<br />-    `queryId`-consulta\_identificador de la consulta devuelta.<br />-    `regressedPlanId`-plan_id del plan devuelta.<br />-   `regressedPlanExecutionCount`-Se detectó número de ejecuciones de la consulta devueltas plan antes de la regresión.<br />-    `regressedPlanAbortedCount`-Número de errores detectados durante la ejecución del plan devuelta.<br />-    `regressedPlanCpuTimeAverage`-Tiempo de CPU medio utilizado por la consulta devuelta antes de que se detecte la regresión.<br />-    `regressedPlanCpuTimeStddev`-Se detectó la desviación estándar de de tiempo de CPU utilizado por la consulta devuelta antes de la regresión.<br />-    `recommendedPlanId`-plan_id del plan al que se debería forzar.<br />-   `recommendedPlanExecutionCount`-Número de ejecuciones de la consulta con el plan que se debería forzar antes de que se detecte la regresión.<br />-    `recommendedPlanAbortedCount`-Número de errores detectados durante la ejecución del plan al que se debería forzar.<br />-    `recommendedPlanCpuTimeAverage`-Promedio tiempo de CPU utilizado por la consulta ejecutada con el plan que se debería forzar (calculado antes de que se detecta la regresión).<br />-    `recommendedPlanCpuTimeStddev`Se detectó la desviación estándar de tiempo de CPU utilizado por la consulta devuelta antes de la regresión.<br /><br />`implementationDetails`<br />-  `method`-El método que se debe usar para corregir la regresión. Valor es siempre `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)]secuencia de comandos que se debe ejecutar para forzar el plan recomendado. |
  
## <a name="remarks"></a>Comentarios  
 Información devuelta por `sys.dm_db_tuning_recommendations` se actualiza cuando el motor de base de datos identifica posibles regresión del rendimiento de consultas y no se conserva. Las recomendaciones se mantienen solo hasta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia. Los administradores de base de datos deben realizar periódicamente copias de seguridad de la recomendación de optimización si desean conservarla después de reciclar el servidor. 

 `currentValue`campo en la `state` columna puede tener los valores siguientes:
 | Estado | Description |
 |--------|-------------|
 | `Active` | Recomendación está activa y no ha aplicado. Usuario puede tomar el script de recomendación y ejecutarlo manualmente. |
 | `Verifying` | Recomendación se aplica por [!INCLUDE[ssde_md](../../includes/ssde_md.md)] y proceso de comprobación internos compara el rendimiento del plan forzado con el plan devuelta. |
 | `Success` | Recomendación se ha aplicado correctamente. |
 | `Reverted` | Recomendación se revirtió porque no hay ningún aumento significativo del rendimiento. |
 | `Expired` | Recomendación ha expirado y no se puede aplicar ya. |

Documento JSON en `state` columna contiene la razón que describe por qué es la recomendación en el estado actual. Los valores en el campo motivo podrían ser: 

| Reason | Description |
|--------|-------------|
| `SchemaChanged` | Recomendación ha caducado porque se cambia el esquema de una tabla que se hace referencia. |
| `StatisticsChanged`| Recomendación expirado debido al cambio de estadísticas en una tabla que se hace referencia. |
| `ForcingFailed` | No se puede forzar el plan recomendada en una consulta. Buscar el `last_force_failure_reason` en el [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) vista para averiguar el motivo del error. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`opción está deshabilitada por el usuario durante el proceso de comprobación. Habilitar `FORCE_LAST_GOOD_PLAN` mediante la opción [AUTOMATIC_TUNING del conjunto de base de datos de ALTER &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) instrucción o forzar el plan manualmente mediante la secuencia de comandos en `[details]` columna. |
| `UnsupportedStatementType` | No se puede forzar el plan en la consulta. Ejemplos de consultas no admitidos son los cursores y `INSERT BULK` instrucción. |
| `LastGoodPlanForced` | Recomendación se ha aplicado correctamente. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identifica posibles regresión del rendimiento, pero la `FORCE_LAST_GOOD_PLAN` opción no está habilitada: vea [AUTOMATIC_TUNING del conjunto de base de datos de ALTER &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplique la recomendación manualmente o habilitar `FORCE_LAST_GOOD_PLAN` opción. |
| `VerificationAborted`| Proceso de comprobación se anula debido al reinicio o Liberador de espacio en el almacén de consultas. |
| `VerificationForcedQueryRecompile`| Se vuelve a compilar en la consulta porque no hay ninguna mejora significativa del rendimiento. |
| `PlanForcedByUser`| Usuario forzar manualmente el plan mediante [sp_query_store_force_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) procedimiento. |
| `PlanUnforcedByUser` | Usuario unforced manualmente el plan mediante [sp_query_store_unforce_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) procedimiento. |

 Estadística en la columna de detalles no se muestran las estadísticas del plan de runtime (por ejemplo, tiempo de CPU actual). Los detalles de recomendación se realizan en el momento de la detección de regresión y describir por qué [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regresión del rendimiento. Use `regressedPlanId` y `recommendedPlanId` a consulta [vistas de catálogo del almacén de consultas](../../relational-databases/performance/how-query-store-collects-data.md) para buscar las estadísticas del plan de exacto en tiempo de ejecución.

## <a name="using-tuning-recommendations-information"></a>Uso de información de las recomendaciones de optimización  
 Puede utilizar la siguiente consulta para obtener el script T-SQL que se solucionará el problema:  
 
```
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 Para obtener más información acerca de las funciones JSON que puede usarse para consultar los valores en la vista de recomendación, consulte [compatibilidad de JSON](../../relational-databases/json/index.md) en [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la `Server admin` o un `Azure Active Directory admin` cuenta.  
  
## <a name="see-also"></a>Vea también  
 [El ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Compatibilidad de JSON](../../relational-databases/json/index.md)
 
