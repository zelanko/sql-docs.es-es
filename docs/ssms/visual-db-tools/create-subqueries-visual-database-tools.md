---
title: Crear subconsultas (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e33ba032dd39c6a476098160dfc95c97998989b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-subqueries-visual-database-tools"></a>Crear subconsultas (Visual Database Tools)
Puede utilizar los resultados de una consulta como entrada para otra consulta. Puede usar los resultados de una subconsulta como una instrucción que utiliza la función IN( ), el operador EXISTS o la cláusula FROM.  
  
Puede crear una subconsulta escribiéndola directamente en el panel SQL o copiando una consulta y pegándola en otra.  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>Para definir una subconsulta en el panel SQL  
  
1.  Cree la consulta principal.  
  
2.  En el panel SQL, seleccione la instrucción SQL y use **Copiar** para mover la consulta al Portapapeles.  
  
3.  Inicie la nueva consulta y después utilice **Pegar** para mover la primera consulta a la cláusula WHERE o FROM de la nueva consulta.  
  
    Imagine, por ejemplo, que tiene dos tablas, `products` y `suppliers`y desea crear una consulta en la que se muestren todos los productos de todos los proveedores suecos. Cree la primera consulta en la tabla `suppliers` para buscar todos los proveedores suecos:  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
    Utilice el comando Copiar para mover esta consulta al Portapapeles. Cree la segunda consulta utilizando la tabla `products` , con la información necesaria sobre los productos:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
    En el panel SQL, agregue una cláusula WHERE a la segunda consulta y, a continuación, pegue la primera consulta del Portapapeles. Escriba la primera consulta entre paréntesis, de forma que el resultado final tenga un aspecto similar al siguiente:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>Vea también  
[Tipos de consultas compatibles &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
