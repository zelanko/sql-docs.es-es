---
title: DROP FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_INDEX_TSQL
- DROP FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- deleting full-text indexes
- removing full-text indexes
- full-text indexes [SQL Server], removing
- DROP FULLTEXT INDEX statement
- dropping full-text indexes
ms.assetid: 7443a4ab-1d43-4a22-bbba-a07f620892cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 09fe23c827b1d3d4561a4333180ad3eb508a3adc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68044242"
---
# <a name="drop-fulltext-index-transact-sql"></a>DROP FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita un índice de texto completo de una vista indizada o una tabla especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP FULLTEXT INDEX ON table_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 Se trata del nombre de la tabla o vista indizada que contiene el índice de texto completo que se va quitar.  
  
## <a name="remarks"></a>Observaciones  
 No necesita quitar todas las columnas del índice de texto completo para poder utilizar el comando DROP FULLTEXT INDEX.  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener el permiso ALTER en la tabla o vista indizada, o pertenecer al rol fijo de servidor **sysadmin** o los roles fijos de base de datos **db_owner** o **db_ddladmin**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita el índice de texto completo de la tabla `JobCandidate`.  
  
```  
USE AdventureWorks2012;  
GO  
DROP FULLTEXT INDEX ON HumanResources.JobCandidate;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
