---
title: El ajuste automático | Microsoft Docs
description: Obtenga información sobre el ajuste automático en SQL Server y Azure SQL Database
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db7fc8514fadbcf9be5b98c85457b4cddeac82cb
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559142"
---
# <a name="automatic-tuning"></a>Ajuste automático
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  El ajuste automático es una característica de base de datos que proporciona información de los posibles problemas de rendimiento de las consultas, recomienda soluciones y corrige automáticamente los problemas identificados.

El ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] le avisa cada vez que se detecta un posible problema de rendimiento y le permite aplicar acciones correctivas o permite el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corregir automáticamente problemas de rendimiento.
El ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] permite identificar y corregir problemas de rendimiento causados por **las regresiones de elección de plan SQL**. El ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] crea los índices necesarios y quita los índices no usados.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] supervisa las consultas que se ejecutan en la base de datos y mejora automáticamente el rendimiento de la carga de trabajo. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tiene un mecanismo de inteligencia integrada que puede ajustar y mejorar el rendimiento de las consultas mediante la adaptación dinámica de la base de datos para la carga de trabajo automáticamente. Hay dos características de ajuste automático que están disponibles:

 -  **Corrección automática de planes** (disponible en [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica los planes de ejecución de consultas problemáticas y problemas de rendimiento del plan de correcciones de SQL.
 -  **Administración automática de índices** (sólo disponible en [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica los índices que se deben agregar en la base de datos y los índices que se deben quitar.

## <a name="why-automatic-tuning"></a>¿Por qué el ajuste automático?

Tres de las principales tareas de administración de base de datos clásica están supervisando la carga de trabajo, que identifica críticos [!INCLUDE[tsql_md](../../includes/tsql-md.md)] realiza una consulta, los índices que deben ser agregados para mejorar el rendimiento e identificación usa con poca frecuencia. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] Proporciona una visión detallada de las consultas y los índices que necesita para supervisar. Sin embargo, supervisar constantemente una base de datos es una tarea ardua y tediosa, especialmente al tratar con muchas bases de datos. Administrar un gran número de bases de datos podría ser imposible de realizar eficazmente. En lugar de supervisar y ajustar manualmente la base de datos, puede delegar algunas de la supervisión y ajuste las acciones a [!INCLUDE[ssde_md](../../includes/ssde_md.md)] mediante la característica de ajuste automático.

### <a name="how-does-automatic-tuning-work"></a>¿Cómo funciona optimización automática?

El ajuste automático es un proceso de análisis que constantemente aprende sobre las características de la carga de trabajo y la supervisión continua e identificar posibles problemas y mejoras.

![Proceso de ajuste automático](./media/tuning-process.png)

Este proceso permite la base de datos para adaptarse dinámicamente a la carga de trabajo mediante la búsqueda de qué índices y planes pueden mejorar el rendimiento de las cargas de trabajo y qué índices afectan a las cargas de trabajo. Según estos hallazgos, el ajuste automático aplica a las acciones de optimización que mejoran el rendimiento de la carga de trabajo. Además, base de datos supervisa continuamente el rendimiento después de cualquier cambio realizado por el ajuste automático para asegurarse de que mejora el rendimiento de la carga de trabajo. Cualquier acción que no mejore el rendimiento se revierte automáticamente. Este proceso de comprobación es una característica clave que garantiza que cualquier cambio realizado por el ajuste automático no disminuya el rendimiento de la carga de trabajo.

## <a name="automatic-plan-correction"></a>Corrección automática de planes

Corrección automática de planes es una característica de ajuste automático que identifica **regresión de elección de planes SQL** y corregir automáticamente el problema al forzar el último plan correcto conocido.

### <a name="what-is-sql-plan-choice-regression"></a>¿Qué es la regresión de elección del plan SQL?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] Puede usar distintos planes SQL para ejecutar el [!INCLUDE[tsql_md](../../includes/tsql-md.md)] las consultas. Los planes de consulta dependen de las estadísticas de índices y otros factores. El plan óptimo que debe usarse para ejecutar algunas [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consulta podría cambiar con el tiempo. En algunos casos, el nuevo plan no podría ser mejor que el anterior y el nuevo plan puede provocar una regresión del rendimiento.

 ![Regresión de elección de plan SQL](media/plan-choice-regression.png "regresión de elección de plan SQL") 

Cada vez que tenga en cuenta la regresión de elección del plan, debe buscar algunos buenos anteriores plan y forzarlo en lugar de usar una actual `sp_query_store_force_plan` procedimiento.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] en [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] proporciona información sobre devueltas planes y recomienda acciones correctivas.
Además, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] le permite automatizar este proceso totalmente y permiten [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corregir cualquier problema detectado relacionados con los cambios del plan.

### <a name="automatic-plan-choice-correction"></a>Corrección de la elección automática de planes

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] puede cambiar automáticamente para el último plan bueno conocido siempre que se detecte la regresión de elección del plan.

![Corrección de elección del plan SQL](media/force-last-good-plan.png "corrección de elección del plan SQL") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta automáticamente cualquier regresión posible de elección de plan incluido el plan que se debe usar en lugar del plan incorrecto.
Cuando el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] aplica el último plan bueno conocido, supervisa automáticamente el rendimiento del plan forzado. Si el plan forzado no es mejor que el plan con regresión, el nuevo plan será forzado y el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compilará un nuevo plan. Si [!INCLUDE[ssde_md](../../includes/ssde_md.md)] comprueba que el plan forzado es mejor que con regresión, el plan forzado se conservará hasta volver a compilar (por ejemplo, en el próximo cambio de esquema o de estadísticas) si es mejor que el plan con regresión.

Nota: Cualquier automática de planes forzado hacer no persit en un reinicio de la instancia de SQL Server.

### <a name="enabling-automatic-plan-choice-correction"></a>Habilitar la corrección de la elección automática de planes

Puede habilitar el ajuste automático por base de datos y especificar que se debería forzar el último plan bueno siempre que se detecte alguna regresión de cambio de plan. El ajuste automático se habilita con el siguiente comando:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
Una vez activada esta opción, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automáticamente forzará cualquier recomendación donde la ganancia de CPU estimada es superior a 10 segundos, o el número de errores en el nuevo plan es mayor que el número de errores del plan recomendado y compruebe que el plan forzado es mejor que la actual.

### <a name="alternative---manual-plan-choice-correction"></a>Alternativa: corrección elección del plan manual

Sin el ajuste automático, los usuarios deberán supervisar el sistema de forma periódica y buscar las consultas con regresión. Si cualquier plan con regresión, el usuario debería encontrarlo algunos buenos anteriores plan y forzarlo en lugar de usar una actual `sp_query_store_force_plan` procedimiento. El procedimiento recomendado sería forzar el último buen plan conocido porque los planes anteriores podrían no ser válidos debido a cambios de índice o estadística. El usuario que fuerza el último buen plan conocido debe supervisar el rendimiento de la consulta que se ejecuta con el plan forzado y comprobar dicho plan forzado funciona según lo previsto. Según los resultados del análisis y supervisión, se debería forzar el plan o el usuario debería encontrarlo alguna otra forma de optimizar la consulta.
Los planes forzados manualmente no se deberían forzar para siempre, porque el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] debería poder aplicar los planes óptimos. El usuario o el DBA debería finalmente no forzar el plan mediante `sp_query_store_unforce_plan` procedimiento y permita que el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] encontrar el plan óptimo.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona todas las vistas necesarias y los procedimientos necesarios para supervisar el rendimiento y corregir problemas en la consulta Store.

En [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], puede encontrar las regresiones de elección del plan mediante vistas de consulta Store del sistema. En [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta y muestra los posibles regresiones de elección de plan y las acciones recomendadas que deben aplicarse en el [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) vista. La vista muestra información sobre el problema, la importancia del problema y los detalles como la consulta identificada, el identificador del plan con regresión, el identificador del plan que se usó como línea base para la comparación y el [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrucción que se puede ejecutar para corregir el problema.

| Tipo | description | DATETIME | score | detalles | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Tiempo de CPU ha cambiado de ms de 4 a 14 ms | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tiempo de CPU ha cambiado de 37 ms a ms 84 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

En la lista siguiente se describen algunas columnas de esta vista:
 - Tipo de la acción recomendada: `FORCE_LAST_GOOD_PLAN`.
 - Descripción que contiene información sobre por qué [!INCLUDE[ssde_md](../../includes/ssde_md.md)] considera que este cambio de plan es una regresión del rendimiento potencial.
 - Fecha y hora cuando se detecta la regresión posibles.
 - Puntuación de esta recomendación. 
 - Detalles sobre los problemas, como el identificador del plan detectado, identificador del plan con regresión, identificador del plan que se debería forzar a corregir el problema, [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script que pueda tener aplicado para corregir el problema, etcetera. Los detalles se almacenan en [formato JSON](../../relational-databases/json/index.md).

Use la siguiente consulta para obtener un script que corrige el problema y obtener información adicional sobre el estimado obtener:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | script | consulta\_Id. | plan actual\_Id. | recomienda plan\_Id. | Estimado\_obtener | error\_propensos a
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cambiado de 3 ms a 46 ms de tiempo de CPU | 36 | EXEC sp\_consulta\_almacenar\_forzar\_plan de 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` representa el número estimado de segundos que se guardarán si el plan recomendado se ejecutaría en lugar del plan actual. Se debe forzar que el plan recomendado en lugar del plan actual si el aumento es mayor que 10 segundos. Si hay más errores (por ejemplo, los tiempos de espera o ejecuciones anuladas) en el plan actual a la recomendada en el plan de la columna `error_prone` se establecería en el valor `YES`. Plan propensas a errores es otro motivo por qué se debería forzar el plan recomendado en lugar de la actual.

Aunque [!INCLUDE[ssde_md](../../includes/ssde_md.md)] proporciona toda la información necesaria para identificar las regresiones de elección del plan; una supervisión continua y corregir problemas de rendimiento puede ser un proceso tedioso. El ajuste automático facilita este proceso.

Nota: Los datos en esta DMV no se conservan después de reiniciar la instancia de SQL Server.

## <a name="automatic-index-management"></a>Administración automática de índices

En [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], administración de índices es fácil porque [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] aprende sobre la carga de trabajo y se asegura de que los datos se indizan siempre de forma óptima. Diseño adecuado de índices es fundamental para un rendimiento óptimo de la carga de trabajo y administración automática de índices puede ayudar a optimizar los índices. Administración automática de índices puede corregir problemas de rendimiento en las bases de datos indexadas incorrectamente, o se mantienen y mejore los índices en el esquema de base de datos existente. El ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] realiza las acciones siguientes:

 - Identifica los índices que podrían mejorar el rendimiento de las consultas de Transact-SQL que leen datos de las tablas.
 - Identifica los índices redundantes o que no se usaron en el período de tiempo que se va a quitar. Quitar índices innecesarios mejora el rendimiento de las consultas que actualizan los datos en tablas.

### <a name="why-do-you-need-index-management"></a>¿Por qué necesita administración de índices?

Los índices aceleran algunas de las consultas que leen datos de las tablas; Sin embargo, puede ralentizar las consultas que actualizan los datos. Debe analizar cuidadosamente cuándo se debe crear un índice y qué columnas debe incluir en el índice. Algunos índices que no sean necesarios más tarde. Por lo tanto, deberá identificar y quitar los índices que no reporten ventajas periódicamente. Si omite los índices no usados, el rendimiento de las consultas que actualizan datos podría reducirse sin ninguna ventaja para las consultas que leen los datos. Los índices no usados también afectan al rendimiento general del sistema porque las actualizaciones adicionales necesitan tareas de registro innecesarias.

Encontrar el conjunto óptimo de índices que mejoren el rendimiento de las consultas que leen datos de las tablas y tener un impacto mínimo en las actualizaciones podría requerir un análisis complejo y continuado.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] usos de inteligencia integrada y reglas avanzadas que analizar las consultas, identificar los índices que serían óptimos para las cargas de trabajo actuales y podrían quitarse los índices. La base de datos de SQL Azure garantiza que tiene un conjunto mínimo necesario de índices para optimizar las consultas que leen datos, con menor impacto en las otras consultas.

### <a name="automatic-index-management"></a>Administración automática de índices

Además de la detección, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] puede aplicar automáticamente recomendaciones identificadas. Si encuentra que las reglas integradas mejoran el rendimiento de la base de datos, podría dejar que [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] administre automáticamente los índices.

Para habilitar el ajuste automático en Azure SQL Database y dejar que la característica de ajuste automático administrar por completo la carga de trabajo, consulte [habilitar el ajuste automático en Azure SQL Database mediante Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).

Cuando el [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] se aplica una recomendación de la instrucción CREATE INDEX o DROP INDEX, supervisa automáticamente el rendimiento de las consultas que se ven afectados por el índice. Se conservarán el nuevo índice solo si se han mejorado el rendimiento de las consultas afectadas. El índice eliminado se automáticamente volverá a crear si hay algunas consultas que se ejecutan más lentamente debido a la ausencia del índice.

### <a name="automatic-index-management-considerations"></a>Consideraciones sobre la administración automática de índices

Acciones necesarias para crear los índices necesarios en [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] podría consumir recursos y afectar temporalmente al rendimiento de la carga de trabajo. Para minimizar el impacto de la creación de índices en el rendimiento de carga de trabajo, Azure SQL Database busca el período de tiempo adecuado para cualquier operación de administración de índice. Acción de ajuste se pospuso si la base de datos necesita recursos para ejecutar la carga de trabajo y se inicia cuando la base de datos tiene suficientes recursos no utilizados que se pueden usar para la tarea de mantenimiento. Una característica importante de la administración automática de índices es una comprobación de las acciones. Cuando Azure SQL Database crea o quita el índice, un proceso de supervisión analiza el rendimiento de la carga de trabajo para comprobar que la acción se ha mejorado el rendimiento. Si no ha reportado una mejora considerable, inmediatamente se revierte la acción. De este modo, Azure SQL Database garantiza que las acciones automáticas no afectar negativamente al rendimiento de la carga de trabajo. Los índices creados por el ajuste automático son transparentes para la operación de mantenimiento en el esquema subyacente. Los cambios de esquema, como quitar o cambiar el nombre de columnas no estén bloqueados por la presencia de índices creados automáticamente. Los índices creados automáticamente por Azure SQL Database se quitan inmediatamente cuando relacionados con la tabla o columnas se quita.

### <a name="alternative---manual-index-management"></a>Alternativa: la administración manual de índices

Sin administración automática de índices, usuario tendría que consultar manualmente [sys.dm_db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) vista para encontrar los índices que podrían mejorar el rendimiento, creación de índices mediante los detalles se proporcionan en esta vista y manualmente supervisar el rendimiento de la consulta. Para encontrar los índices que se deben quitar, los usuarios deben supervisar las estadísticas de uso operativo de los índices a los índices de búsqueda que se usa con poca frecuencia.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] simplifica este proceso. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] analiza la carga de trabajo, identifica las consultas que podrían ejecutarse más rápido con un nuevo índice y se identifican los índices no usados o duplicados. Obtener más información sobre la identificación de los índices que deben cambiarse [buscar recomendaciones de índices en Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Vea también  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funciones JSON](../../relational-databases/json/index.md)
