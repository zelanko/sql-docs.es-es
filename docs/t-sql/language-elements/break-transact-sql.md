---
title: BREAK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BREAK
- BREAK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- exiting innermost loop [SQL Server]
- END keyword
- ignored statements
- BREAK keyword
ms.assetid: 67c30b8d-3f15-41ad-b9a9-a4ced3b2af9f
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 469a374680dc51bb2d8e3aac1306061366a32cfa
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981477"
---
# <a name="break-transact-sql"></a>BREAK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Sale del bucle más interno en una instrucción WHILE o una instrucción IF…ELSE dentro de un bucle WHILE. Se ejecutan las instrucciones que aparecen después de la palabra clave END, que marca el final del bucle. A menudo, pero no siempre, BREAK se inicia mediante una prueba IF.  
  
## <a name="examples"></a>Ejemplos  
  
```  
-- Uses AdventureWorks  
  
WHILE ((SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300)  
BEGIN  
    UPDATE DimProduct  
        SET ListPrice = ListPrice * 2;  
     IF ((SELECT MAX(ListPrice) FROM dbo.DimProduct) > $500)  
         BREAK;  
END  
```  
  
## <a name="see-also"></a>Ver también  
 [Lenguaje de control de flujo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


