---
title: IHconstrainttypes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHconstrainttypes_TSQL
- IHconstrainttypes
dev_langs:
- TSQL
helpviewer_keywords:
- IHconstrainttypes system table
ms.assetid: 955d6fa9-0b31-4335-a3cd-e4c4d90ad308
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4d24c94cc4c6dca00fc0e3fd9cd93626da6e4fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076451"
---
# <a name="ihconstrainttypes-transact-sql"></a>IHconstrainttypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHconstrainttypes** tabla del sistema contiene una fila por cada tipo de restricción que no son de SQL Server admitido para publicadores que no son: SQL Server. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**type**|**nvarchar(255)**|El nombre de un tipo de restricción que no es de SQL Server compatible.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
