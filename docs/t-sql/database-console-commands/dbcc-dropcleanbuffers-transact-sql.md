---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1a7a1507e230995df1c2b67a8499a12270b535c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Quita todos los búferes borrados del grupo de búferes y los objetos de almacén de columnas desde el grupo de objetos de almacén de columnas.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis
Sintaxis para SQL Server: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Sintaxis de almacenamiento de SQL Azure y almacenamiento de datos en paralelo:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información. Mensajes informativos siempre se suprimen en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 COMPUTE  
 Purgar la caché del plan de consulta de cada nodo de ejecución.  
  
 ALL  
 Purgar la caché del plan de consulta de cada nodo de ejecución y desde el nodo de Control. Este es el valor predeterminado si no especifica un valor.  
  
## <a name="remarks"></a>Comentarios  
Utilice DBCC DROPCLEANBUFFERS para probar consultas con una caché de búferes COLD sin apagar y reiniciar el servidor.
Para quitar búferes borrados de los objetos de grupo y almacén de columnas del búfer desde el grupo de objetos de almacén de columnas, en primer lugar utilice CHECKPOINT para crear una caché de búferes cold. Así se obliga a que todas las páginas desfasadas de la base de datos actual se escriban en el disco y se borren los búferes. Una vez hecho esto, puede emitir el comando DBCC DROPCLEANBUFFERS para quitar todos los búferes del grupo de búferes.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC DROPCLEANBUFFERS en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  

Se aplica a: SQL Server, almacenamiento de datos paralelos 

- Requiere la pertenencia al rol fijo de servidor **sysadmin** .  

Se aplica a: Azure SQL Data Warehouse

- Requiere la pertenencia al rol fijo de servidor DB_OWNER.  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  

