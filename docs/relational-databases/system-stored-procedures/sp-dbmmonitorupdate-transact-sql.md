---
title: sp_dbmmonitorupdate (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2970c0c6f75755e295fae32a1a5ceab046bb75d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza la tabla de estado del monitor de creación de reflejos de la base de datos insertando una nueva fila de tabla para cada base de datos reflejada y trunca las filas más antiguas que el período de retención actual. El período de retención predeterminado es de 7 días (168 horas). Cuando se actualiza la tabla, **sp_dbmmonitorupdate** evalúa las métricas de rendimiento.  
  
> [!NOTE]  
>  La primera vez **sp_dbmmonitorupdate** se ejecuta, crea la tabla de estado de creación de reflejo de la base de datos y la **dbm_monitor** rol fijo de base de datos en el **msdb** base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos para la que se va a actualizar el estado de la creación de reflejos. Si *database_name* no se especifica, el procedimiento actualiza la tabla de estado para cada base de datos reflejada en la instancia del servidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_dbmmonitorupdate** se puede ejecutar solo en el contexto de la **msdb** base de datos.  
  
 Si una columna de la tabla de estado no se aplica al rol de un asociado, el valor es NULL en ese asociado. Una columna también tendrá un valor NULL si la información relevante no está disponible, como durante una conmutación por error o un reinicio del servidor.  
  
 Después de **sp_dbmmonitorupdate** crea el **dbm_monitor** rol fijo de base de datos en el **msdb** la base de datos, los miembros de la **sysadmin** rol fijo de servidor puede agregar a cualquier usuario la **dbm_monitor** rol fijo de base de datos. El **dbm_monitor** rol permite a sus miembros ver el estado de creación de reflejo de la base de datos pero no actualizarla, pero no ver o configurar eventos de creación de reflejo de la base de datos.  
  
 Al actualizar el estado de creación de reflejo de una base de datos, **sp_dbmmonitorupdate** inspecciona el último valor de cualquier métrica de rendimiento de creación de reflejo para el que se ha especificado un umbral de advertencia. Si el valor supera el umbral, el procedimiento agrega un evento informativo al registro de eventos. Todos los valores son promedios desde la última actualización. Para obtener más información, vea [Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se actualiza el estado de la creación de reflejos solo para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
