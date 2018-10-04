---
title: sp_dbmmonitorresults (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54cf9a13396674c2ac9dd43845c94d7ac657f008
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702753"
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve filas de estado para una base de datos supervisada de la tabla de estado en la que está almacenado el historial de supervisión de la creación de reflejo de la base de datos y permite elegir si el procedimiento obtiene antes el estado más reciente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Especifica la base de datos para la que se debe devolver el estado de la creación de reflejos.  
  
 *rows_to_return*  
 Especifica la cantidad de filas devueltas:  
  
 0 = Última fila  
  
 1 = Filas devueltas en las dos últimas horas  
  
 2 = Filas devueltas en las cuatro últimas horas  
  
 3 = Filas devueltas en las ocho últimas horas  
  
 4 = Filas devueltas el último día  
  
 5 = Filas devueltas los dos últimos días  
  
 6 = 100 últimas filas  
  
 7 = último 500 filas  
  
 8 = último 1.000 filas  
  
 9 = Último millón de filas  
  
 *update_status*  
 Especifica que, antes de devolver resultados, el procedimiento:  
  
 0 = No actualiza el estado de la base de datos. Los resultados se calculan utilizando únicamente las dos últimas filas, cuya antigüedad depende de cuándo se actualizó la tabla de estado.  
  
 1 = actualiza el estado de la base de datos mediante una llamada a **sp_dbmmonitorupdate** antes de calcular los resultados. Sin embargo, si se ha actualizado la tabla de estado dentro de los 15 segundos anteriores, o el usuario no es un miembro de la **sysadmin** rol fijo de servidor **sp_dbmmonitorresults** se ejecuta sin actualizar el estado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el número solicitado de filas de estado del historial para la base de datos especificada. Cada fila contiene la siguiente información:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nombre de una base de datos reflejada.|  
|**Rol**|**int**|Rol de creación de reflejos actual de la instancia del servidor:<br /><br /> 1 = Entidad de seguridad<br /><br /> 2 = Reflejo|  
|**mirroring_state**|**int**|Estado de la base de datos:<br /><br /> 0 = suspensión<br /><br /> 1 = desconectada<br /><br /> 2 = En proceso de sincronización<br /><br /> 3 = Pendiente de conmutación por error<br /><br /> 4 = Sincronizada|  
|**witness_status**|**int**|El estado de conexión del testigo en la sesión de creación de reflejo de la base de datos puede ser:<br /><br /> 0 = Desconocido<br /><br /> 1 = Conectado<br /><br /> 2 = Desconectado|  
|**log_generation_rate**|**int**|Cantidad (en kilobytes/seg.) de registro generado desde la actualización anterior del estado de la creación de reflejos de esta base de datos.|  
|**unsent_log**|**int**|Tamaño (en kilobytes) del registro no enviado en la cola de envío del servidor principal.|  
|**send_rate**|**int**|Tasa de envío (en kilobytes/seg.) del registro desde el servidor principal al servidor reflejado.|  
|**unrestored_log**|**int**|Tamaño (en kilobytes) de la cola de puesta al día en el servidor reflejado.|  
|**recovery_rate**|**int**|Tasa de puesta al día (en kilobytes/seg.) en el servidor reflejado.|  
|**transaction_delay**|**int**|Retardo total (en milisegundos) para todas las transacciones.|  
|**transactions_per_sec**|**int**|Número de transacciones por segundo en la instancia del servidor principal.|  
|**average_delay**|**int**|Retardo medio en la instancia del servidor principal para cada transacción a causa de la creación de reflejo de la base de datos. En modo de alto rendimiento (es decir, cuando se establece la propiedad SAFETY en OFF), este valor suele ser 0.|  
|**time_recorded**|**datetime**|Hora a la que la fila fue registrada por el monitor de creación de reflejo de la base de datos. Es la hora del reloj del sistema del servidor principal.|  
|**time_behind**|**datetime**|Hora aproximada del reloj del sistema del servidor principal a la que está asociada actualmente la base de datos reflejada. Este valor solo es significativo en la instancia del servidor principal.|  
|**local_time**|**datetime**|Hora del reloj del sistema en la instancia local del servidor a la que se actualizó esta fila.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_dbmmonitorresults** se puede ejecutar solo en el contexto de la **msdb** base de datos.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **sysadmin** rol fijo de servidor o en el **dbm_monitor** rol fijo de base de datos en el **msdb** base de datos. El **dbm_monitor** rol permite a sus miembros ver el estado, la creación de reflejo de la base de datos, pero no actualizarlo, pero no ver o configurar los eventos de creación de reflejo de la base de datos.  
  
> [!NOTE]  
>  La primera vez que **sp_dbmmonitorupdate** se ejecuta, crea el **dbm_monitor** rol fijo de base de datos en el **msdb** base de datos. Los miembros de la **sysadmin** rol fijo de servidor puede agregar a cualquier usuario la **dbm_monitor** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve las filas registradas durante las dos horas anteriores sin actualizar el estado de la base de datos.  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
