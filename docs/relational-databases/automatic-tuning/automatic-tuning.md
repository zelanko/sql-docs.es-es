---
title: El ajuste automático | Documentos de Microsoft
description: Obtener información sobre el ajuste automático de SQL Server y base de datos de SQL Azure
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 0e77a1d7e24fa2635b3e699672338e588c1f5c1c
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707773"
---
# <a name="automatic-tuning"></a>Ajuste automático
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  El ajuste automático es una característica de base de datos que proporciona información de los posibles problemas de rendimiento de las consultas, recomienda soluciones y corrige automáticamente los problemas identificados.

El ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] le notifica cada vez que se detecta un posible problema de rendimiento y le permite aplicar acciones correctivas o permite el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] reparar automáticamente problemas de rendimiento.
El ajuste automático [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] le permite identificar y corregir problemas de rendimiento causados por **las regresiones de elección de plan SQL**. El ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] crea índices necesarios y quita los índices no usados.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] supervisa las consultas que se ejecutan en la base de datos y mejora el rendimiento de la carga de trabajo automáticamente. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] dispone de un mecanismo de inteligencia incorporada que puede optimizar y mejorar el rendimiento de las consultas dinámicamente adaptando la base de datos para la carga de trabajo automáticamente. Hay dos características de optimización automática que están disponibles:

 -  **Corrección automática plan** (disponible en [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] y [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica los planes de ejecución de consultas problemáticas y correcciones SQL plan los problemas de rendimiento.
 -  **Administración de índices automática** (sólo disponible en [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) que identifica los índices que se deben agregar en la base de datos e índices que se deben quitar.

## <a name="why-automatic-tuning"></a>¿Por qué el ajuste automático?

Una de las principales tareas de administración clásico de la base de datos está supervisando la carga de trabajo, identificar crítico [!INCLUDE[tsql_md](../../includes/tsql_md.md)] realiza una consulta, los índices que se deben agregar para mejorar el rendimiento y usan índices con poca frecuencia. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] Proporciona una visión detallada de las consultas y los índices que necesita supervisar. Sin embargo, al supervisar constantemente la base de datos es una tarea tediosa y disco duro, especialmente cuando se trabaja con muchas bases de datos. Administrar un gran número de bases de datos podría ser imposible de realizar eficazmente. En lugar de supervisión y optimización de la base de datos manualmente, puede delegar algunas de la supervisión y optimización acciones a [!INCLUDE[ssde_md](../../includes/ssde_md.md)] mediante la característica de optimización automática.

### <a name="how-does-automatic-tuning-works"></a>¿Cómo funciona la optimización automática?

El ajuste automático es un proceso de análisis que constantemente se obtiene información acerca de la característica de la carga de trabajo y la supervisión continua e identificar posibles problemas y mejoras.

![Proceso de optimización automática](./media/tuning-process.png)

Este proceso permite a la base de datos para adaptarse dinámicamente a la carga de trabajo mediante la búsqueda de los índices y los planes pueden mejorar el rendimiento de las cargas de trabajo y qué índices afectan a las cargas de trabajo. En función de estos resultados, el ajuste automático aplica a acciones de optimización que mejoran el rendimiento de la carga de trabajo. Además, base de datos supervisa continuamente el rendimiento después de cualquier cambio realizado por el ajuste automático para asegurarse de que mejora el rendimiento de la carga de trabajo. Automáticamente se revierte cualquier acción que no mejora el rendimiento. Este proceso de comprobación es una característica clave que garantiza que cualquier cambio realizado por el ajuste automático no disminuya el rendimiento de la carga de trabajo.

## <a name="automatic-plan-correction"></a>Corrección automática de plan

Corrección automática de plan es una característica de optimización automática que identifica **regresión de elección de planes SQL** y corregir automáticamente ese problema forzando el último plan buena conocido.

### <a name="what-is-sql-plan-choice-regression"></a>¿Qué es la regresión de elección de plan SQL?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] Puede usar distintos planes SQL para ejecutar el [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consultas. Planes de consulta dependen de las estadísticas, índices y otros factores. El plan óptimo que debe utilizarse para ejecutar algunas [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consulta se puede cambiar con el tiempo. En algunos casos, el nuevo plan no podría ser mejor que el anterior y el nuevo plan puede provocar una regresión del rendimiento.

 ![Regresión de elección de plan SQL](media/plan-choice-regression.png "regresión de elección de plan SQL") 

Cada vez que se tenga en cuenta la regresión de elección de plan, debería encontrar algunos buenos anteriores plan y forzar en lugar de la actual mediante una `sp_query_store_force_plan` procedimiento.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] en [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] proporciona información sobre devueltas planes y las acciones correctivas recomendadas.
Además, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] le permite automatizar este proceso completo y permiten [!INCLUDE[ssde_md](../../includes/ssde_md.md)] corregir cualquier problema detectado relacionados con los cambios del plan.

### <a name="automatic-plan-choice-correction"></a>Corrección de elección de plan automática

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] puede cambiar automáticamente para el último plan buenos conocido cuando se detecta la regresión de elección de plan.

![Corrección de elección de plan SQL](media/force-last-good-plan.png "corrección de elección de plan SQL") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta automáticamente cualquier posible regresión de elección de plan que incluye el plan que se debe usar en lugar del plan incorrecto.
Cuando el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] se aplica la última conoce buen plan, supervisa automáticamente el rendimiento del plan forzado. Si el plan forzado no es mejor que el plan devuelta, el nuevo plan será unforced y [!INCLUDE[ssde_md](../../includes/ssde_md.md)] se compilará un nuevo plan. Si [!INCLUDE[ssde_md](../../includes/ssde_md.md)] comprueba que el plan forzado es mejor que una devuelta, el plan forzado se conservarán hasta que una nueva compilación (por ejemplo, en el próximo cambio de esquema o estadísticas) si es mejor que el plan devuelta.

Nota: Cualquier automática planes forzada no no persit en un reinicio de la instancia de SQL Server.

### <a name="enabling-automatic-plan-choice-correction"></a>Habilitar la corrección de elección de plan automática

Puede habilitar el ajuste automático por base de datos y especificar que se debería forzar el último plan bueno siempre que se detecte alguna regresión de cambio de plan. El ajuste automático se habilita con el siguiente comando:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
Una vez que activar esta opción, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automáticamente forzará cualquier recomendación donde la ganancia de CPU estimada es superior a 10 segundos, o el número de errores en el nuevo plan es mayor que el número de errores en el plan recomendado y compruebe que el plan forzado es mejor que el actual.

### <a name="alternative---manual-plan-choice-correction"></a>Alternativa - corrección de elección de plan manual

Sin el ajuste automático, los usuarios deberán supervisar el sistema de forma periódica y buscar las consultas con regresión. Si cualquier plan devueltas, usuario debería encontrar algunos buenos anteriores plan y forzar en lugar de la actual mediante una `sp_query_store_force_plan` procedimiento. La práctica recomendada sería forzar el último plan buena conocido porque planes anteriores pueden no ser válidos debido a cambios de índice o estadística. El usuario que fuerza el último plan buena conocido debe supervisar el rendimiento de la consulta que se ejecuta con el plan forzado y comprobar dicho plan forzado funciona según lo previsto. Según los resultados de la supervisión y el análisis, se debería forzar el plan o usuario debería encontrar alguna otra forma de optimizar la consulta.
Planes forzados manualmente no se deberían forzar indefinidamente, porque el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] debería poder aplicar los planes óptimo. El usuario o el DBA debe finalmente eliminar la aplicación del plan mediante `sp_query_store_unforce_plan` procedimiento y permita que el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] encontrar el plan óptimo.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona todos los procedimientos necesarios para supervisar el rendimiento y corregir problemas en el almacén de consultas y vistas es necesarias.

En [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], puede encontrar las regresiones de elección del plan mediante vistas de sistema de almacén de consultas. En [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], [!INCLUDE[ssde_md](../../includes/ssde_md.md)] detecta y se muestran posibles regresiones de elección del plan y las acciones recomendadas que deben aplicarse en el [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) vista. La vista muestra información sobre el problema, la importancia del problema y los detalles como la consulta identificada, el identificador del plan devuelta, el identificador del plan que se usó como línea base para la comparación y el [!INCLUDE[tsql_md](../../includes/tsql_md.md)] instrucción que se puede ejecutar para corregir el problema.

| Tipo | description | DATETIME | score | detalles | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Tiempo de CPU cambiado de ms 4 a 14 ms | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tiempo de CPU cambiado de 37 ms a ms 84 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

En la lista siguiente se describen algunas columnas de esta vista:
 - Tipo de la acción recomendada: `FORCE_LAST_GOOD_PLAN`.
 - Descripción que contiene información sobre por qué [!INCLUDE[ssde_md](../../includes/ssde_md.md)] considera que este cambio de plan es una regresión del rendimiento potencial.
 - Fecha y hora cuando se detecta la regresión posible.
 - Puntuación de esta recomendación. 
 - Obtener más información acerca de los problemas, como el identificador del plan, identificador del plan devuelta, Id. del plan al que se debería forzar a corregir el problema detectado [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 secuencia de comandos que podría aplicarse para corregir el problema, etcetera. Los detalles de [formato JSON](../../relational-databases/json/index.md).

Use la siguiente consulta para obtener un script que corrige el problema e información adicional sobre estimado obtener:

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

| reason | score | script | consulta\_Id. | plan actual\_Id. | recomienda plan\_Id. | Estimado\_obtener | error\_propensas a
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Tiempo de CPU cambiado de 3 ms a ms 46 | 36 | EXEC sp\_consulta\_almacenar\_forzar\_plan 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` representa el número estimado de segundos que se ahorraría si el plan recomendado se ejecutaría en lugar del plan actual. El plan recomendado se debería forzar en lugar del plan actual si el aumento es mayor que 10 segundos. Si hay más errores (por ejemplo, los tiempos de espera o anuladas ejecuciones) en el plan actual que en tal como se recomienda planear, la columna `error_prone` se establecería en el valor `YES`. Plan propensas a errores es otro motivo por qué se debería forzar el plan recomendado en lugar del actual.

Aunque [!INCLUDE[ssde_md](../../includes/ssde_md.md)] proporciona toda la información necesaria para identificar las regresiones de elección del plan; continuo de supervisión y corregir problemas de rendimiento puede ser una tarea tediosa. El ajuste automático facilita este proceso.

Nota: Los datos en esta DMV no se conservan después de un reinicio de la instancia de SQL Server.

## <a name="automatic-index-management"></a>Administración automática de índice

En [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], la administración de índices es fácil porque [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] obtiene información acerca de la carga de trabajo y se asegura de que los datos se indizan siempre un rendimiento óptimo. Diseño de índices adecuados es fundamental para un rendimiento óptimo de la carga de trabajo y administración de índices automática puede ayudar a optimizar los índices. Administración automática del índice puede corregir problemas de rendimiento en las bases de datos indizadas incorrectamente, o se mantienen y mejore los índices en el esquema de base de datos existente. El ajuste automático [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] realiza las siguientes acciones:

 - Identifica los índices que podrían mejorar el rendimiento de las consultas de T-SQL que leen datos de las tablas.
 - Identifica los índices redundantes o que no se usaron en el período de tiempo que se va a quitar. Quitar índices innecesarios mejora el rendimiento de las consultas que actualizan los datos en tablas.

### <a name="why-do-you-need-index-management"></a>¿Por qué necesita la administración de índices?

Acelerar algunas de las consultas que leen datos de las tablas; Sin embargo, podrían ralentizar las consultas que actualizan los datos. Debe analizar cuidadosamente cuándo se debe crear un índice y qué columnas debe incluir en el índice. Algunos índices no pueden ser necesaria más tarde. Por lo tanto, se necesitaría identificar y quitar los índices que no proporcionan las ventajas de periódicamente. Si omite los índices sin usar, rendimiento de las consultas que actualizan los datos podría reducirse sin ninguna ventaja en las consultas que leen los datos. Índices no usados también afectan al rendimiento general del sistema porque actualizaciones adicionales necesitan un registro innecesario.

Buscar el conjunto óptimo de índices que mejoren el rendimiento de las consultas que leer los datos de las tablas y tiene un impacto mínimo en las actualizaciones puede requerir análisis complejo y continuado.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] inteligencia incorporada de usos y reglas avanzadas que analizar las consultas, identificar los índices que sean óptimos para las cargas de trabajo actuales y podrían desaparecer los índices. La base de datos de SQL Azure se asegura de que tiene un conjunto mínimo necesario de índices que optimizar las consultas que leen los datos, con un impacto minimizado en otras consultas.

### <a name="automatic-index-management"></a>Administración automática de índice

Además de la detección, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] pueden aplicar automáticamente las recomendaciones identificadas. Si encuentra que las reglas integradas de mejoran el rendimiento de la base de datos, puede permitir que [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] administrar automáticamente los índices.

Para habilitar el ajuste automático de la base de datos de SQL Azure y permitir que la característica de optimización automática totales para administrar la carga de trabajo, consulte [habilitar el ajuste automático de la base de datos de SQL de Azure mediante el portal de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).

Cuando el [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] se aplica una recomendación de CREATE INDEX o DROP INDEX, automáticamente supervisa el rendimiento de las consultas que se ven afectados por el índice. Nuevo índice se mantendrá solo si se han mejorado el rendimiento de las consultas afectadas. El índice eliminado se creará automáticamente si hay algunas consultas que se ejecutan más lentamente debido a la ausencia del índice.

### <a name="automatic-index-management-considerations"></a>Consideraciones sobre la administración automática de índice

Las acciones necesarias para crear los índices necesarios en [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] puede consumir recursos y temporalmente afectan al rendimiento de la carga de trabajo. Para minimizar el impacto de la creación de índices en el rendimiento de la carga de trabajo, base de datos de SQL Azure busca el período de tiempo adecuado para cualquier operación de administración de índice. Acción para la optimización se pospone si la base de datos necesita recursos para ejecutar la carga de trabajo e inicia cuando la base de datos tiene suficientes recursos no utilizados que se pueden usar para la tarea de mantenimiento. Una característica importante de la administración de índices automática es una comprobación de las acciones. Cuando la base de datos de SQL Azure crea o quita el índice, un proceso de supervisión analiza el rendimiento de la carga de trabajo para comprobar que la acción de mejora el rendimiento. Si lo no aportar mejora considerable, inmediatamente se revierte la acción. De esta manera, la base de datos de SQL Azure garantiza que acciones automáticas no afectar negativamente al rendimiento de la carga de trabajo. Índices creados por el ajuste automático son transparentes para la operación de mantenimiento en el esquema subyacente. Cambios de esquema, como quitar o cambiar el nombre de las columnas no estén bloqueados por la presencia de índices creados de forma automática. Índices creados automáticamente por base de datos de SQL Azure se quitan inmediatamente cuando relacionados con la tabla o columnas se quita.

### <a name="alternative---manual-index-management"></a>Alternativa - administración de índices manual

Sin la administración automática del índice, el usuario necesitaría consultar manualmente [sys.dm_db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) vista para buscar índices que pueden mejorar el rendimiento, crear índices con los detalles se proporcionan en esta vista y manualmente supervisar el rendimiento de la consulta. Para buscar los índices que se deben eliminar, los usuarios deben supervisar las estadísticas de uso operativo de los índices a los índices de búsqueda que se usa con poca frecuencia.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] simplifica este proceso. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] analiza la carga de trabajo, identifica las consultas que pudieron ejecutarse más rápidamente con un nuevo índice e identifica los índices no usados o duplicados. Obtener más información acerca de la identificación de los índices que deben cambiarse en [buscar recomendaciones de índices en el portal de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Vea también  
 [AUTOMATIC_TUNING de conjunto de base de datos de ALTER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funciones JSON](../../relational-databases/json/index.md)
