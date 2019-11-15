---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 6fda5419756689df6b9be1fda9a792c14229c1ce
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632842"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Haga clic en un producto.

En la siguiente fila, haga clic en cualquier nombre de producto que le interese. Al hacer clic, en esta página web se muestra otro contenido, adecuado para el producto que seleccione.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[Instancia administrada de<br />SQL Database](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>Instancia administrada de SQL Server y SQL Database

Crea un grupo de cargas de trabajo del regulador de recursos y asocia el grupo de cargas de trabajo a un grupo de recursos de servidor del regulador de recursos. Resource Governor no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxis

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>Argumentos

*group_name*     
Es el nombre definido por el usuario para identificar el grupo de cargas de trabajo. *group_name* es alfanumérico, puede tener hasta 128 caracteres, debe ser único dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y debe cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).

IMPORTANCE = { LOW | **MEDIUM** | HIGH }     
Especifica la importancia relativa de una solicitud en el grupo de cargas de trabajo. La importancia puede ser una de las siguientes, siendo MEDIUM el valor predeterminado:

- LOW
- MEDIUM (predeterminado)
- HIGH

> [!NOTE]
> Internamente, cada valor de IMPORTANCE se almacena como un número que se usa para los cálculos.

IMPORTANCE es local para el grupo de recursos de servidor; los grupos de cargas de trabajo de importancia distinta dentro del mismo grupo de recursos de servidor se influyen entre sí, pero no influyen en los grupos de cargas de trabajo de otro grupo de recursos de servidor.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*     
Especifica la cantidad máxima de memoria que una única solicitud puede tomar del grupo. *valor* es un porcentaje relativo al tamaño del grupo de recursos de servidor especificado por MAX_MEMORY_PERCENT. 

El elemento *value* es un entero hasta [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], y un elemento de float a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. El valor predeterminado es de 25. El intervalo permitido para *value* es de 1 a 100.

> [!NOTE]  
> La cantidad especificada se refiere únicamente a la memoria concedida para la ejecución de la consulta.  
  
> [!IMPORTANT]
> Establecer *valor* en 0 evita la ejecución de consultas con operaciones SORT y HASH JOIN en grupos de cargas de trabajo definidos por el usuario.     
>
> No se recomienda establecer el elemento *value* en un valor superior a 70 porque es posible que el servidor no pueda reservar memoria suficiente si se están ejecutando otras consultas simultáneas. Esto puede dar lugar al final a un error de tiempo de espera de consulta 8645.      
  
> [!NOTE]  
> Si los requisitos de memoria de consulta superan el límite especificado por este parámetro, el servidor hace lo siguiente:  
>   
> -  En el caso de los grupos de cargas de trabajo definidos por el usuario, el servidor intenta reducir el grado de paralelismo de consulta hasta que el requisito de memoria cae por debajo del límite, o hasta que el grado de paralelismo sea igual a 1. Si el requisito de memoria de consulta sigue siendo mayor que el límite, se produce el error 8657.  
>   
> -  En el caso de los grupos de cargas de trabajo internos y predeterminados, el servidor permite que la consulta obtenga la memoria necesaria.  
>   
> Tenga en cuenta que ambos casos están sujetos a un error de tiempo de espera 8645 si el servidor no tiene suficiente memoria física.  

REQUEST_MAX_CPU_TIME_SEC = *value*     
Especifica la cantidad máxima de tiempo de CPU, en segundos, que puede usar una solicitud. *valor* debe ser 0 o un entero positivo. El valor predeterminado de *value* es 0, que indica una cantidad ilimitada.

> [!NOTE]
> De forma predeterminada, Resource Governor no evita que una solicitud continúe si se supera el tiempo máximo. Sin embargo, se generará un evento. Para obtener más información, vea [Clase de eventos Umbral de la CPU superado](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).     

> [!IMPORTANT]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3, y si se usa la [marca de seguimiento 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), Resource Governor anula una solicitud cuando se supera el tiempo máximo.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*     
Especifica el tiempo máximo, en segundos, que una consulta puede esperar hasta que esté disponible una concesión de memoria (memoria de búfer de trabajo). *valor* debe ser 0 o un entero positivo. El valor predeterminado de *valor*, 0, usa un cálculo interno basado en el costo de la consulta para determinar el tiempo máximo.

> [!NOTE]
> Una consulta no tiene por qué generar un error cuando se agota el tiempo de espera para la concesión de memoria. Solo se producirá un error si se ejecutan demasiadas consultas simultáneamente. De lo contrario, es posible que la consulta obtenga la concesión de memoria mínima, lo que reducirá su rendimiento.

MAX_DOP = *value*     
Especifica el **grado máximo de paralelismo (MAXDOP)** para la ejecución de consultas en paralelo. *valor* debe ser 0 o un entero positivo. El intervalo permitido para *value* es de 0 a 64. El valor predeterminado para *valor*, 0, usa la configuración global. MAX_DOP se trata de la siguiente manera:

> [!NOTE]
> El valor MAX_DOP del grupo de cargas de trabajo reemplaza la [configuración del servidor para el grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) y la [configuración con ámbito de base de datos](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) **MAXDOP**.

> [!TIP]
> Para realizar esta acción en el nivel de consulta, use la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) **MAXDOP**. Establecer el grado máximo de paralelismo como una sugerencia de consulta es eficaz siempre que no supere el valor MAX_DOP del grupo de cargas de trabajo. Si el valor de la sugerencia de consulta MAXDOP supera el valor configurado mediante Resource Governor, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa el valor `MAX_DOP` de Resource Governor. La [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) MAXDOP siempre reemplaza la [configuración del servidor para el grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).      
>   
> Para lograr esto en el nivel de base de datos, use la [configuración con ámbito de base de datos](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) **MAXDOP**.      
>   
> Para lograr esto en el nivel de servidor, use la [opción de configuración del servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) **Grado máximo de paralelismo (MAXDOP)** .     

GROUP_MAX_REQUESTS = *value*     
Especifica el número máximo de solicitudes simultáneas que pueden ejecutarse en el grupo de cargas de trabajo. *valor* debe ser 0 o un entero positivo. El valor predeterminado de *valor* es 0 y permite solicitudes ilimitadas. Cuando se alcanza el máximo de solicitudes simultáneas, un usuario de ese grupo puede iniciar sesión, pero se coloca en estado de espera hasta que las solicitudes simultáneas caigan por debajo del valor especificado.

USING { *pool_name* |  **"default"** }     
Asocia el grupo de cargas de trabajo al grupo de recursos de servidor definido por el usuario identificado por *pool_name*. De esta forma, el grupo de cargas de trabajo se coloca en el grupo de recursos de servidor. Si no se proporciona *pool_name* o si no se usa el argumento USING, el grupo de cargas de trabajo se coloca en el grupo predeterminado de Resource Governor predefinido.

"default" es una palabra reservada y cuando se utiliza con USING, debe incluirse entre comillas ("") o corchetes ([]).

> [!NOTE]
> Todos los grupos de cargas de trabajo y de recursos de servidor predefinidos usan nombres en minúsculas, como "predeterminado". Debe tenerse esto en cuenta en los servidores que usan una intercalación que distingue entre mayúsculas y minúsculas. En los servidores que usan una intercalación que no distingue entre mayúsculas y minúsculas, como SQL_Latin1_General_CP1_CI_AS, los nombres "predeterminado" y "Predeterminado" son equivalentes.

EXTERNAL external_pool_name | "default"     
**Se aplica a** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).

El grupo de cargas de trabajo puede especificar un grupo de recursos externos. Se puede definir un grupo de cargas de trabajo y asociarlo con dos grupos:

- Un grupo de recursos para cargas de trabajo y consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Un nuevo grupo de recursos para procesos externos. Para obtener más información, vea [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="remarks"></a>Notas
Cuando se utiliza `REQUEST_MEMORY_GRANT_PERCENT`, se permite que la creación de índices use más memoria del área de trabajo que la concedida inicialmente para mejorar el rendimiento. El regulador de recursos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite este tratamiento especial. Sin embargo, la concesión inicial y cualquier concesión de memoria adicional están limitadas por la configuración del grupo de cargas de trabajo y el grupo de recursos de servidor.

El límite de `MAX_DOP` se establece por [tarea](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). No es un límite por [solicitud](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ni por consulta. Esto significa que durante una ejecución de consultas en paralelo, una sola solicitud puede generar varias tareas que se asignan a un [programador](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Para más información, consulte la [guía de arquitectura de subprocesos y tareas](../../relational-databases/thread-and-task-architecture-guide.md).

Cuando se usa `MAX_DOP` y la consulta en tiempo de compilación se marca como serie, no podrá volver a establecerse como paralela en tiempo de ejecución, independientemente del grupo de cargas de trabajo o del valor de configuración del servidor. Una vez que se configura `MAX_DOP`, solo se puede reducir debido a la presión de memoria. La reconfiguración del grupo de cargas de trabajo no es visible mientras se espera en la cola de concesión de memoria.

### <a name="index-creation-on-a-partitioned-table"></a>Creación de índices en una tabla con particiones

La memoria usada para la creación de índices en una tabla con particiones no alineada es proporcional al número de particiones involucradas. Si la memoria total necesaria supera el límite por consulta `REQUEST_MAX_MEMORY_GRANT_PERCENT` impuesto por la configuración del grupo de cargas de trabajo de Resource Governor, puede que esta creación de índices no se ejecute. Dado que el grupo de cargas de trabajo *"predeterminado"* permite que una consulta supere el límite por consulta con la memoria mínima necesaria, es posible que el usuario pueda ejecutar la misma creación de índices en el grupo de cargas de trabajo *"predeterminado"* si el grupo de recursos de servidor *"predeterminado"* tiene configurada una memoria total suficiente para ejecutar dicha consulta.

## <a name="permissions"></a>Permisos
Requiere el permiso `CONTROL SERVER`.

## <a name="example"></a>Ejemplo

Cree un grupo de cargas de trabajo denominado `newReports`, que usa la configuración predeterminada de Resource Governor y está en el grupo predeterminado de Resource Governor. El ejemplo especifica el grupo `default`, pero no es necesario.

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>Consulte también

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[Instancia administrada de<br />SQL Database](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse"></a>SQL Data Warehouse 

CREATE WORKLOAD GROUP (Transact-SQL) (versión preliminar) crea un grupo de cargas de trabajo.  Los grupos de cargas de trabajo son contenedores de un conjunto de solicitudes y son la base de la configuración de la administración de cargas de trabajo en un sistema.  Los grupos de cargas de trabajo proporcionan la capacidad de reservar recursos para el aislamiento de la carga de trabajo, contienen recursos, definen recursos por solicitud y cumplen las reglas de ejecución.  Una vez completada la instrucción, la configuración entra en vigor.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

```
CREATE WORKLOAD GROUP group_name  
 WITH  
 (        MIN_PERCENTAGE_RESOURCE = value  
      ,   CAP_PERCENTAGE_RESOURCE = value 
      ,   REQUEST_MIN_RESOURCE_GRANT_PERCENT = value   
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]  
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )  
  [ ; ]
```

*group_name*</br>
Especifica el nombre por el que se identifica el grupo de cargas de trabajo.  group_name es sysname.  Puede tener hasta 128 caracteres y debe ser único en la instancia.

*MIN_PERCENTAGE_RESOURCE* = value</br>
Especifica una asignación de recursos mínima garantizada para este grupo de cargas de trabajo que no se comparte con otros grupos de cargas de trabajo.  value es un intervalo de números enteros comprendido entre 0 y 100.  La suma de min_percentage_resource en todos los grupos de cargas de trabajo no puede ser superior a 100.  El valor de min_percentage_resource no puede ser mayor que cap_percentage_resource.  Hay valores efectivos mínimos permitidos por nivel de servicio.  Vea Valores efectivos<link> para obtener más detalles.

*CAP_PERCENTAGE_RESOURCE* = value</br>
Especifica el uso máximo de recursos para todas las solicitudes de un grupo de cargas de trabajo.  El intervalo permitido para value es de 1 a 100.  El valor de cap_percentage_resource debe ser mayor que min_percentage_resource.  Se puede reducir el valor efectivo de cap_percentage_resource si min_percentage_resource se configura mayor que cero en otros grupos de cargas de trabajo.

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
Establece la cantidad mínima de recursos asignados por solicitud.  value es un parámetro necesario con un intervalo decimal entre 0,75 y 100,00.  El valor de request_min_resource_grant_percent debe ser un múltiplo de 0,25, debe ser un factor de min_percentage_resource y ser menor que cap_percentage_resource.  Hay valores efectivos mínimos permitidos por nivel de servicio.  Vea Valores efectivos<link> para obtener más detalles.

Por ejemplo:

```sql
CREATE WORKLOAD GROUP wgSample WITH  
( MIN_PERCENTAGE_RESOURCE = 26              -- integer value
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
 ,CAP_PERCENTAGE_RESOURCE = 100 )
```

Tenga en cuenta los valores que se usan para las clases de recursos como directriz para request_min_resource_grant_percent.  La tabla siguiente contiene las asignaciones de recursos para Gen2.

|Clase de recurso|Porcentaje de recursos|
|---|---|
|Smallrc|3 %|
|Mediumrc|10 %|
|Largerc|22 %|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>
Establece la cantidad máxima de recursos asignados por solicitud.  value es un parámetro opcional con un valor predeterminado igual a request_min_resource_grant_percent.  value debe ser mayor o igual que request_min_resource_grant_percent.  Cuando el valor de request_max_resource_grant_percent es mayor que request_min_resource_grant_percent y los recursos del sistema están disponibles, se asignan recursos adicionales a una solicitud.

*IMPORTANCE* = { LOW |  BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>
Especifica la importancia predeterminada de una solicitud para el grupo de cargas de trabajo.  Importance puede ser una de las siguientes, siendo NORMAL el valor predeterminado:
- LOW
- BELOW_NORMAL
- NORMAL (valor predeterminado)
- ABOVE_NORMAL
- HIGH  

La importancia establecida en el grupo de cargas de trabajo está predeterminada para todas las solicitudes en el grupo de cargas de trabajo.  Un usuario también puede establecer la importancia en el nivel de clasificador, lo que puede invalidar la configuración de importancia del grupo de cargas de trabajo.  Esto permite diferenciar la importancia de las solicitudes de un grupo de cargas de trabajo para acceder a los recursos no reservados más rápido.  Cuando la suma de min_percentage_resource entre grupos de cargas de trabajo es inferior a 100, hay recursos no reservados que se asignan en función de la importancia.

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>
Especifica el tiempo máximo, en segundos, que se puede ejecutar una consulta antes de que se cancele.  value debe ser 0 o un entero positivo.  El valor predeterminado de value es 0, que indica una cantidad ilimitada.  El tiempo invertido en esperar en la cola de solicitudes no se tiene en cuenta para la ejecución de la consulta.

## <a name="remarks"></a>Notas
Los grupos de cargas de trabajo correspondientes a las clases de recursos se crean automáticamente para favorecer la compatibilidad con versiones anteriores.  Estos grupos de cargas de trabajo definidos por el sistema no se pueden quitar.  Se pueden crear otros 8 grupos de cargas de trabajo definidos por el usuario.

## <a name="effective-values"></a>Valores efectivos

Los parámetros min_percentage_resource, cap_percentage_resource, request_min_resource_grant_percent y request_max_resource_grant_percent tienen valores efectivos que se ajustan en el contexto del nivel de servicio actual y la configuración de otros grupos de cargas de trabajo.

La simultaneidad admitida por nivel de servicio sigue siendo la misma que cuando las clases de recursos se usaban para definir concesiones de recursos por consulta; por lo tanto, los valores admitidos para request_min_resource_grant_percent dependen del nivel de servicio en el que se establece la instancia.  En el nivel de servicio más bajo, se admite la simultaneidad DW100c, 4.  El valor de request_min_resource_grant_percent efectivo de un grupo de cargas de trabajo configurado puede ser un 25 % o superior.  Vea esta tabla para más información.

|Nivel de servicio|Número máximo de consultas concurrentes|% mínimo admitido para REQUEST_MIN_RESOURCE_GRANT_PERCENT y MIN_PERCENTAGE_RESOURCE|
|---|---|---|
|DW100c|4|25 %|
|DW200c|8|12,5 %|
|DW300c|12|8 %|
|DW400c|16|6,25 %|
|DW500c|20|5 %|
|DW1000c|32|3 %|
|DW1500c|32|3 %|
|DW2000c|48|2 %|
|DW2500c|48|2 %|
|DW3000c|64|1,5 %|
|DW5000c|64|1,5 %|
|DW6000c|128|0,75 %|
|DW7500c|128|0,75 %|
|DW10000c|128|0,75 %|
|DW15000c|128|0,75 %|
|DW30000c|128|0,75 %|
||||

De forma similar, request_min_resource_grant_percent, min_percentage_resource debe ser mayor o igual que el valor de request_min_resource_grant_percent efectivo.  Un grupo de cargas de trabajo con un valor de min_percentage_resource configurado menor que el valor efectivo de min_percentage_resource tiene el valor ajustado en cero en tiempo de ejecución.  Cuando esto sucede, los recursos configurados para min_percentage_resource se pueden compartir entre todos los grupos de cargas de trabajo.  Por ejemplo, el grupo de cargas de trabajo wgAdHoc con un valor de min_percentage_resource del 10 % que se ejecuta en Dw1000c y tendría un valor de min_percentage_resource efectivo del 10 % (3,25 % es el valor mínimo admitido en DW1000c).  wgAdhoc en DW100c tendría un valor de min_percentage_resource efectivo del 0 %.  El 10 % configurado para wgAdhoc se compartiría entre todos los grupos de cargas de trabajo.

Cap_percentage_resource también tiene un valor efectivo.  Si se configura un grupo de cargas de trabajo wgAdhoc con un cap_percentage_resource del 100 % y otro grupo de cargas de trabajo wgDashboards se crea con un 25 % min_percentage_resource, el valor de cap_percentage_resource efectivo de wgAdhoc se convierte en 75 %.

La forma más fácil de comprender los valores en tiempo de ejecución para los grupos de cargas de trabajo es consultar la vista del sistema [sys.dm_workload_management_workload_groups_stats] (../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md?view=azure-sqldw-latest).

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL DATABASE

## <a name="see-also"></a>Vea también
[DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)

::: moniker-end
