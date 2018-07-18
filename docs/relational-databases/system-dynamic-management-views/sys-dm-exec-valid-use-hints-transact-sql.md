---
title: Sys.dm_exec_valid_use_hints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
caps.latest.revision: 5
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d1fb0ffed04c77e280d02378429cf769107bdfbc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987147"
---
# <a name="sysdmexecvalidusehints-transact-sql"></a>Sys.dm_exec_valid_use_hints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Devuelve [USE HINT](../../t-sql/queries/hints-transact-sql-query.md) admite nombres de sugerencia. Muestra un nombre de sugerencia por fila.  
  
Utilice esta DMV para ver la lista de todas las sugerencias de admitidos en la notación de USE HINT.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|El nombre de la sugerencia.|

Consulte [sugerencias de consulta](../../t-sql/queries/hints-transact-sql-query.md) para obtener descripciones de cada sugerencia.

Introducido en [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1.
  
## <a name="see-also"></a>Vea también  
    
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

