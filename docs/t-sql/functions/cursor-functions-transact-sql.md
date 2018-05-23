---
title: Funciones del cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9c3919edabc5d0a642571f833680747a4b8bb3cc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="cursor-functions-transact-sql"></a>Funciones del cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Estas funciones escalares devuelven información sobre los cursores:
  
|||  
|-|-|  
|[@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)|[CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)|  
|[@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)||  
  
Todas las funciones del cursor son no deterministas. En otras palabras, estas funciones no siempre devuelven el mismo resultado cada vez que se ejecutan, incluso con el mismo conjunto de valores de entrada. Vea [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md) para obtener más información sobre el determinismo de las funciones.
  
## <a name="see-also"></a>Vea también
[Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
  
  
