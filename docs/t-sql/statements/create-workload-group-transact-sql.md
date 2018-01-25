---
title: Crear grupo de cargas de trabajo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE WORKLOAD GROUP statement
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
caps.latest.revision: "47"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cec1360259d78679fab31a45a074d5fbbf3779b5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un grupo de cargas de trabajo del regulador de recursos y asocia el grupo de cargas de trabajo a un grupo de recursos de servidor del regulador de recursos. Regulador de recursos no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
 Es el nombre definido por el usuario para identificar el grupo de cargas de trabajo. *nombre_grupo* es alfanumérico, puede tener hasta 128 caracteres, deben ser únicos dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 IMPORTANCIA = {BAJO | **MEDIO** | ALTA}  
 Especifica la importancia relativa de una solicitud en el grupo de cargas de trabajo. La importancia puede ser una de las siguientes, siendo MEDIUM el valor predeterminado:  
  
-   LOW  
-   MEDIUM (predeterminado)    
-   HIGH  
  
> [!NOTE]  
> Internamente, cada valor de IMPORTANCE se almacena como un número que se usa para los cálculos.  
  
 IMPORTANCE es local para el grupo de recursos de servidor; los grupos de cargas de trabajo de importancia distinta dentro del mismo grupo de recursos de servidor se influyen entre sí, pero no influyen en los grupos de cargas de trabajo de otro grupo de recursos de servidor.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*value*  
 Especifica la cantidad máxima de memoria que una única solicitud puede tomar del grupo. Este porcentaje es relativo al tamaño del grupo de recursos de servidor especificado por MAX_MEMORY_PERCENT.  
  
> [!NOTE]  
> La cantidad especificada se refiere únicamente a la memoria concedida para la ejecución de la consulta.  
  
 *valor* debe ser 0 o un entero positivo. El intervalo permitido para *valor* está comprendido entre 0 y 100. El valor predeterminado de *valor* es 25.  
  
 Observe lo siguiente:  
  
-   Establecer *valor* en 0 impide que las consultas con las operaciones de ordenación y HASH JOIN en grupos de cargas de trabajo definido por el usuario ejecute.  
  
-   No se recomienda configuración *valor* superior a 70 porque el servidor puede ser no se puede reservar suficiente memoria libre si están ejecutando otras consultas simultáneas. Esto puede dar lugar al final a un error de tiempo de espera de consulta 8645.  
  
> [!NOTE]  
>  Si los requisitos de memoria de consulta superan el límite especificado por este parámetro, el servidor hace lo siguiente:  
>   
>  En el caso de los grupos de cargas de trabajo definidos por el usuario, el servidor intenta reducir el grado de paralelismo de consulta hasta que el requisito de memoria cae por debajo del límite, o hasta que el grado de paralelismo sea igual a 1. Si el requisito de memoria de consulta sigue siendo mayor que el límite, se produce el error 8657.  
>   
>  En el caso de los grupos de cargas de trabajo internos y predeterminados, el servidor permite que la consulta obtenga la memoria necesaria.  
>   
>  Tenga en cuenta que ambos casos están sujetos a un error de tiempo de espera 8645 si el servidor no tiene suficiente memoria física.  
  
 REQUEST_MAX_CPU_TIME_SEC =*value*  
 Especifica la cantidad máxima de tiempo de CPU, en segundos, que puede usar una solicitud. *valor* debe ser 0 o un entero positivo. El valor predeterminado de *valor* es 0, lo que significa ilimitado.  
  
> [!NOTE]  
> De forma predeterminada, el regulador de recursos no impedirá una solicitud continuar si se supera el tiempo máximo. Sin embargo, se generará un evento. Para obtener más información, consulte [CPU umbral de esta clase de eventos](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).  

> [!IMPORTANT]
> A partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 y el uso de [2422 marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), el regulador de recursos se anulará una solicitud cuando se supera el tiempo máximo. 
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 Especifica el tiempo máximo, en segundos, que una consulta puede esperar a que una concesión de memoria (memoria de búfer de trabajo) esté disponible.  
  
> [!NOTE]  
>  Una consulta no tiene por qué generar un error cuando se agota el tiempo de espera para la concesión de memoria. Solo se producirá un error si se ejecutan demasiadas consultas simultáneamente. De lo contrario, es posible que la consulta obtenga la concesión de memoria mínima, lo que reducirá su rendimiento.  
  
 *valor* debe ser 0 o un entero positivo. El valor predeterminado de *valor*, 0, utiliza un cálculo interno basado en el costo de consulta para determinar el tiempo máximo.  
  
 MAX_DOP =*value*  
 Especifica el grado máximo de paralelismo (DOP) para las solicitudes paralelas. *valor* debe ser 0 o un entero positivo. El intervalo permitido para *valor* está comprendido entre 0 y 64. El valor predeterminado de *valor*, 0, utiliza la configuración global. MAX_DOP se trata de la siguiente manera:  
  
-   MAX_DOP como sugerencia de consulta resulta eficaz siempre y cuando no supere el MAX_DOP del grupo de cargas de trabajo. Si el valor de la sugerencia de consulta MAXDOP supera el valor configurado mediante el Regulador de recursos, el Motor de base de datos emplea el valor MAXDOP del Regulador de recursos.  
  
-   MAX_DOP como sugerencia de consulta, siempre invalida el 'grado máximo de paralelismo' de sp_configure.  
  
-   MAX_DOP del grupo de cargas de trabajo invalida el 'grado máximo de paralelismo' de sp_configure.  
  
-   Si la consulta en tiempo de compilación se marca como serie, no podrá volver a establecerse como paralela en tiempo de ejecución, independientemente del grupo de cargas de trabajo o del valor de sp_configure.  
  
-   Una vez configurado DOP, solo se puede reducir ante la concesión de presión de memoria. La reconfiguración del grupo de cargas de trabajo no es visible mientras se espera en la cola de concesión de memoria.  
  
 GROUP_MAX_REQUESTS =*value*  
 Especifica el número máximo de solicitudes simultáneas que pueden ejecutarse en el grupo de cargas de trabajo. *valor* debe ser 0 o un entero positivo. El valor predeterminado de *valor*(0) permite un número ilimitadas solicitudes. Cuando se alcanza el máximo de solicitudes simultáneas, un usuario de ese grupo puede iniciar sesión, pero se coloca en estado de espera hasta que las solicitudes simultáneas caigan por debajo del valor especificado.  
  
 USING { *pool_name* | **"default"** }  
 Asocia el grupo de cargas de trabajo con el grupo de recursos definidos por el usuario identificado por *pool_name*. De esta forma, el grupo de cargas de trabajo se coloca en el grupo de recursos de servidor. Si *pool_name* no se proporciona, o si no se usa el argumento USING, el grupo de cargas de trabajo se coloca en el grupo predeterminado de regulador de recursos predefinidos.  
  
 "default" es una palabra reservada y cuando se utiliza con USING, debe incluirse entre comillas ("") o corchetes ([]).  
  
> [!NOTE]  
>  Todos los grupos de cargas de trabajo y de recursos de servidor predefinidos usan nombres en minúsculas, como "predeterminado". Debe tenerse esto en cuenta en los servidores que usan una intercalación que distingue entre mayúsculas y minúsculas. En los servidores que usan una intercalación que no distingue entre mayúsculas y minúsculas, como SQL_Latin1_General_CP1_CI_AS, los nombres "predeterminado" y "Predeterminado" son equivalentes.  
  
 EXTERNAL external_pool_name | “default“  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 Grupo de cargas de trabajo puede especificar un grupo de recursos externos. Puede definir un grupo de cargas de trabajo y asociar con 2 grupos:  
  
-   Un grupo de recursos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargas de trabajo y consultas  
  
-   Un grupo de recursos externo para los procesos externos. Para obtener más información, consulte [sp_execute_external_script &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 REQUEST_MEMORY_GRANT_PERCENT: se permite que la creación de índices use más memoria del área de trabajo que la concedida inicialmente para mejorar el rendimiento. El regulador de recursos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite este tratamiento especial. Sin embargo, la concesión inicial y cualquier concesión de memoria adicional están limitadas por la configuración del grupo de cargas de trabajo y el grupo de recursos de servidor.  
  
 **Creación de índices en una tabla con particiones**  
  
 La memoria consumida por la creación de índice en la tabla con particiones no alineada es proporcional al número de particiones involucradas. Si la memoria total necesaria supera el límite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) impuesto por la configuración del grupo de cargas de trabajo del regulador de recursos, puede que esta creación de índices no se ejecute. Dado que el grupo de cargas de trabajo "predeterminado" permite que una consulta supere el límite por consulta con la memoria mínima necesaria, es posible que el usuario pueda ejecutar la misma creación de índices en el grupo de cargas de trabajo "predeterminado" si el grupo de recursos de servidor "predeterminado" tiene configurada una memoria total suficiente para ejecutar dicha consulta.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo crear un grupo de cargas de trabajo denominado `newReports`. Utiliza la configuración predeterminada del regulador de recursos y está en el grupo predeterminado del regulador de recursos. El ejemplo especifica el grupo `default`, pero no es necesario.  
  
```  
CREATE WORKLOAD GROUP newReports  
    USING "default" ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

