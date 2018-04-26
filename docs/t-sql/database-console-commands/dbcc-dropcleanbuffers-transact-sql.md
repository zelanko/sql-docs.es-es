---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
caps.latest.revision: 35
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2db3b373f941745c87431b08f7bcf099a67fc16
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Quita del grupo de búferes todos los búferes borrados y quita del grupo de objetos de almacén de columnas los objetos de almacén de columnas.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis
Sintaxis para SQL Server: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Sintaxis para Azure SQL Warehouse y Almacenamiento de datos paralelos:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información. Los mensajes informativos siempre se suprimen en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 COMPUTE  
 Purga la caché de datos en memoria de cada nodo de ejecución.  
  
 ALL  
 Purga la caché de datos en memoria de cada nodo de ejecución y del nodo de control. Este es el valor predeterminado si no se especifica ningún valor.  
  
## <a name="remarks"></a>Notas  
Utilice DBCC DROPCLEANBUFFERS para probar consultas con una caché de búferes COLD sin apagar y reiniciar el servidor.
Para quitar del grupo de búferes los búferes borrados y para quitar del grupo de objetos de almacén de columnas los objetos de almacén de columnas, use primero CHECKPOINT para crear una caché de búferes COLD. Así se obliga a que todas las páginas desfasadas de la base de datos actual se escriban en el disco y se borren los búferes. Una vez hecho esto, puede emitir el comando DBCC DROPCLEANBUFFERS para quitar todos los búferes del grupo de búferes.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC DROPCLEANBUFFERS en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  

Se aplica a: SQL Server, Almacenamiento de datos paralelos 

- Requiere la pertenencia al rol fijo de servidor **sysadmin** .  

Se aplica a: Azure SQL Data Warehouse

- Requiere pertenencia al rol fijo de servidor DB_OWNER.  
  
## <a name="see-also"></a>Ver también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
