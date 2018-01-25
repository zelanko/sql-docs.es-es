---
title: DBCC PROCCACHE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs: TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
caps.latest.revision: "31"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 27a247f0900ad39ef77d96a54d68c795dc8f6f07
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Muestra información acerca de la caché de procedimientos en forma de tabla.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 por  
 Permite que se especifiquen opciones.  
  
 NO_INFOMSGS  
 Suprime todos los mensajes informativos que tienen niveles de gravedad entre 0 y 10.  
  
## <a name="remarks"></a>Comentarios  
La caché de procedimientos se utiliza para almacenar en caché los planes compilados y ejecutables con el fin de acelerar la ejecución de lotes. Las entradas de una caché de procedimientos están en el nivel de lote. La caché de procedimientos incluye las siguientes entradas:
-   Planes compilados  
-   Planes de ejecución  
-   Árbol algebraico  
-   Procedimientos extendidos  
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describe las columnas del conjunto de resultados.
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**NUM proc búferes**|Número total de páginas utilizadas por todas las entradas de la caché de procedimientos.|  
|**NUM proc búferes utilizados**|Número total de páginas utilizadas por todas las entradas que se están utilizando actualmente.|  
|**NUM proc curiosidad activa**|Se conserva únicamente por compatibilidad con versiones anteriores. Número total de páginas utilizadas por todas las entradas que se están utilizando actualmente.|  
|**tamaño de la caché de procedimientos**|Número total de entradas de la caché de procedimientos.|  
|**caché de procedimientos que se usa**|Número total de entradas que se están utilizando actualmente.|  
|**caché de procedimientos active**|Se conserva únicamente por compatibilidad con versiones anteriores. Número total de entradas que se están utilizando actualmente.|  
  
## <a name="permissions"></a>Permissions  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
