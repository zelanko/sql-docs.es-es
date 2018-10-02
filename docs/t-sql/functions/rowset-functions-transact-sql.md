---
title: Funciones de conjuntos de filas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], rowsets
- rowsets [SQL Server], functions
- rowsets [SQL Server]
ms.assetid: ac24d700-3144-4ab5-9fa8-8c014001cc71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c843db24866c819babe11c55a24301cdd20146d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735043"
---
# <a name="rowset-functions-transact-sql"></a>Funciones de conjuntos de filas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Las siguientes funciones de conjunto de filas devuelven un objeto que se puede usar en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] en lugar de una referencia de tabla.  
  
|||  
|-|-|  
|[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)|[OPENJSON](../../t-sql/functions/openjson-transact-sql.md)|  
|[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)|[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)|  
|[OPENXML](../../t-sql/functions/openxml-transact-sql.md)||  
  
 Todas las funciones de conjuntos de filas son no deterministas. Por ello, estas funciones no siempre devuelven el mismo resultado cada vez que se invocan, incluso con el mismo conjunto de valores de entrada. Para más información sobre el determinismo de las funciones, vea [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Ver también  
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
