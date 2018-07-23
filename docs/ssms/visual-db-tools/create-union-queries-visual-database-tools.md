---
title: Crear consultas UNION (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 361a54be2c4b92cd0020e0629f8abeef281c0abb
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980147"
---
# <a name="create-union-queries-visual-database-tools"></a>Crear consultas UNION (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
La palabra clave UNION permite incluir los resultados de dos instrucciones SELECT en una única tabla. Todas las filas devueltas desde la instrucción SELECT se combinan como resultado de la expresión UNION. Para ejemplos, consulte [Ejemplos de SELECT (Transact-SQL)](http://msdn.microsoft.com/9b9caa3d-e7d0-42e1-b60b-a5572142186c).  
  
> [!NOTE]  
> En el panel Diagrama solo puede aparecer una cláusula SELECT. Por tanto, cuando trabaje con la consulta UNION, el Diseñador de consultas ocultará el panel de operaciones de tablas.  
  
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
  
## <a name="see-also"></a>Ver también  
[Tipos de consultas compatibles (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](http://msdn.microsoft.com/607c296f-8a6a-49bc-975a-b8d0c0914df7)  
  
