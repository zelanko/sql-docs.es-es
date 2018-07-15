---
title: Crear consultas UNION (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3469f186285d5885e1353b5c8a1f8cffe444e3cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263931"
---
# <a name="create-union-queries-visual-database-tools"></a>Crear consultas UNION (Visual Database Tools)
  La palabra clave UNION permite incluir los resultados de dos instrucciones SELECT en una única tabla. Todas las filas devueltas desde la instrucción SELECT se combinan como resultado de la expresión UNION. Para obtener ejemplos, vea [ejemplos de SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql).  
  
> [!NOTE]  
>  En el panel Diagrama solo puede aparecer una cláusula SELECT. Por tanto, cuando trabaje con la consulta UNION, el Diseñador de consultas ocultará el panel de operaciones de tablas.  
  
### <a name="to-create-a-merged-select-query"></a>Para crear una consulta SELECT mezclada  
  
1.  Abra una consulta o cree una nueva.  
  
2.  En el panel SQL, escriba una expresión UNION válida.  
  
     El ejemplo siguiente es una expresión UNION válida.  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  En el menú **Diseñador de consultas** , haga clic en **Ejecutar SQL** para ejecutar la consulta.  
  
     El Diseñador de consultas da formato a su consulta UNION.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de consultas compatibles &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [Unión &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-operators-union-transact-sql)  
  
  
