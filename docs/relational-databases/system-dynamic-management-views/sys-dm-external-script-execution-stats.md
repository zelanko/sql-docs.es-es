---
title: Sys.dm_external_script_execution_stats | Documentos de Microsoft
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
caps.latest.revision: "5"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a80c26130d5671dd387122930e599a2c33a5db60
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmexternalscriptexecutionstats"></a>sys.dm_external_script_execution_stats
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


  Devuelve una fila por cada tipo de solicitud de script externo. Las solicitudes de script externo se agrupan según el lenguaje compatible del script externo. Se genera una fila para cada función registrada de script externo. Las funciones de script externo arbitrarias no se registran a menos que las envíe un proceso principal, como `rxExec`.

 
  
> [!NOTE]  
>  Esta DMV solo está disponible si ha instalado y después habilitado la característica que admite la ejecución del script externo. Para más información sobre cómo hacer esto para scripts de R, consulte [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) (Configuración de servicios de R de SQL Server).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|language|**nvarchar**|Nombre del lenguaje de script externo registrado. Cada script externo debe especificar el lenguaje en la solicitud de script para iniciar el iniciador asociado. |  
|counter_name|**nvarchar**|Nombre de una función de script externo seleccionada. No admite valores NULL.|  
|counter_value|**integer**|Número total de instancias que en que se ha llamado la función registrada de script externo en el servidor. Este valor es acumulativo, comienza en el momento en que se instaló la característica en la instancia y no se puede restablecer.|  

  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW SERVER STATE en el servidor.  
  
> [!NOTE]  
>  Los usuarios que ejecuten scripts externos deben tener el permiso adicional EXECUTE ANY EXTERNAL SCRIPT, sin embargo, los administradores pueden usar esta DMV sin este permiso. 
  
## <a name="remarks"></a>Notas  
  Esta DMV se proporciona para la telemetría interna, a fin de supervisar el uso general de la nueva característica de ejecución de scripts externos que se proporciona en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. El servicio de telemetría comienza cuando LaunchPad comienza e incrementa un contador basado en disco cada vez que se llama una función registrada de script externo.

Por lo general, los contadores de rendimiento solo son válidos siempre que el proceso que los genera esté activo. Por lo tanto, una consulta en una DMV no puede mostrar datos detallados para servicios que ya no están en ejecución. Por ejemplo, si un iniciador ejecuta scripts externos y los completa muy rápido, una DMV convencional podría no mostrar ningún dato.

Por lo tanto, los contadores a los que esta DMV hace seguimiento siguen en ejecución y se mantiene el estado de sys.dm_external_script_requests mediante escrituras en disco, incluso si la instancia está apagada.

   
  
### <a name="r-counter-values"></a>Valores de contadores de R
 Actualmente el único lenguaje de script externo que se admite en [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] es R. [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] controla las solicitudes de scripts externos para el lenguaje R. 

Para R, esta DMV realiza un seguimiento del número de llamadas de R que se realizan en una instancia. Por ejemplo, si se llama a `rxLinMod` y se ejecuta de manera simultánea, el contador aumenta en 1.
 
En el caso del lenguaje R, los valores del contador que aparecen en el campo *counter_name* representan los nombres de las funciones registradas de ScaleR. Los valores del campo *counter_value* representan los números acumulados de instancias de la función específica de ScaleR. 

La cuenta comienza cuando se instala la característica y se habilita en la instancia, y se acumula hasta que un administrador sobrescribe o elimina el archivo que mantiene el estado. Por lo tanto, generalmente no es posible restablecer los valores en *counter_value*. Si desea supervisar el uso por sesión, tiempos calendario u otros intervalos, le recomendamos registrar los conteos en una tabla.

### <a name="registration-of-external-script-functions"></a>Registro de funciones de scripts externos

El lenguaje R admite scripts arbitrarios y la comunidad de R proporciona muchos miles de paquetes, cada uno de los cuales con sus propias funciones y métodos. Sin embargo, esta DMV supervisa únicamente las funciones de ScaleR que se instalan con SQL Server R Services.

El registro de estas funciones se realiza cuando se instala la característica; además, no se pueden agregar ni borrar funciones registradas.

## <a name="examples"></a>Ejemplos  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>Visualización del número de scripts de R en ejecución en el servidor  
 En el ejemplo siguiente se muestra el número acumulado de ejecuciones de scripts externos para el lenguaje R.  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'R';
```  

  
## <a name="see-also"></a>Ver también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md) 
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

