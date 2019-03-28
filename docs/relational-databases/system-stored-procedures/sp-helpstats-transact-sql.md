---
title: sp_helpstats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6a78ec7a666c40c1c1bd742545139aa2e9ea0aec
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534898"
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información estadística acerca de las columnas e índices de la tabla especificada.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Para obtener información sobre las estadísticas, consulte el [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) y [sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) vistas de catálogo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object_name'` Especifica la tabla en la que se va a proporcionar la información estadística. *object_name* es **nvarchar (520)** y no puede ser null. Se puede especificar un nombre de una o dos partes.  
  
`[ @results = ] 'value'` Especifica la extensión de la información que proporcione. Las entradas válidas son **todas** y **estadísticas**. **Todos los** presenta estadísticas de todos los índices y columnas con estadísticas creadas en ellas; **Estadísticas** solamente presenta estadísticas no asociadas con un índice. *valor* es **nvarchar (5)** con un valor predeterminado es STATS.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 En la tabla siguiente se describen las columnas del conjunto de resultados.  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**statistics_name**|Nombre de la estadística. Devuelve **sysname** y no puede ser null.|  
|**statistics_keys**|Claves en que se basa la estadística. Devuelve **nvarchar (2078)** y no puede ser null.|  
  
## <a name="remarks"></a>Comentarios  
 Utilice DBCC SHOW_STATISTICS para presentar información detallada de estadística acerca de cualquier índice o estadística en particular. Para obtener más información, consulte [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) y [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crean estadísticas de una sola columna en todas las columnas posibles de todas las tablas de usuario de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] mediante `sp_createstats`. A continuación, se ejecuta `sp_helpstats` para buscar las estadísticas de resultado creadas en la tabla `Customer`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
