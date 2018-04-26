---
title: DBCC TRACESTATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
caps.latest.revision: 36
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c85cf36412afdda2e050df6159e52c59e96287bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Muestra el estado de las marcas de seguimiento.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*trace#*  
Es el número de la marca de seguimiento cuyo estado se muestra. Si no se especifican *trace#* ni -1, se muestran todas las marcas de seguimiento habilitadas para la sesión.
  
*n*  
Es una marca de posición que indica que se pueden especificar varias marcas de seguimiento.
  
-1  
Muestra el estado de las marcas de seguimiento habilitadas globalmente. Si se especifica -1 sin *trace#*, se muestran todas las marcas de seguimiento globales habilitadas.
  
WITH NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describe la información del conjunto de resultados.
  
|Nombre de columna|Description|  
|---|---|
|**TraceFlag**|Nombre de la marca de seguimiento.|  
|**Estado**|Indica si la marca de seguimiento está establecida en ON o en OFF, ya sea globalmente o para la sesión.<br /><br /> 1 = ON <br /><br /> 0 = OFF|  
|**Global**|Indica si la marca de seguimiento está establecida globalmente.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Session**|Indica si la marca de seguimiento está establecida para la sesión.<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS devuelve una columna para el número de la marca de seguimiento y otra para el estado. Esto indica si la marca de seguimiento está establecida en ON (1) o en OFF (0). El encabezado de columna para el número de la marca de seguimiento es **Global Trace Flag** o **Session Trace Flag**, según se esté comprobando el estado de una marca de seguimiento global o de sesión.
  
## <a name="remarks"></a>Notas  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hay dos tipos de marcas de seguimiento: sesión y global. Las marcas de seguimiento de sesión se activan para una conexión y solo están visibles para esa conexión. Las marcas de seguimiento globales se establecen en el nivel del servidor y están visibles para todas las conexiones del servidor.
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol **public** .
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se muestra el estado de todas las marcas de seguimiento habilitadas globalmente.
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
En el siguiente ejemplo se muestra el estado de las marcas de seguimiento `2528` y `3205`.
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
En el siguiente ejemplo se muestra si la marca de seguimiento `3205` está habilitada globalmente.
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
En el siguiente ejemplo se muestran todas las marcas de seguimiento habilitadas para la sesión actual.
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>Ver también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
