---
title: "Realización de una consulta a una tabla jerárquica mediante métodos de jerarquía | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af8bdce0dd68fbf33d364757cbb07d60054b1100
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-2-3---querying-a-hierarchical-table-using-hierarchy-methods"></a>Lección 2-3: Realización de una consulta en una tabla jerárquica mediante métodos de jerarquía
Ahora que está totalmente rellena la tabla HumanResources.EmployeeOrg, esta tarea mostrará cómo realizar una consulta en la jerarquía utilizando alguno de los métodos jerárquicos.  
  
### <a name="to-find-subordinate-nodes"></a>Para buscar nodos subordinados  
  
1.  Sariya tiene un empleado subordinado. Para consultar los subordinados de Sariya, ejecute la consulta siguiente que usa el método [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) :  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    El resultado muestra tanto a Sariya como a Wanida. Sariya aparece porque es el descendiente de nivel 0. Wanida es el descendiente de nivel 1.  
  
2.  También se puede consultar esta información mediante el método [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) . `GetAncestor` toma un argumento para el nivel que está intentando devolver. Puesto que Wanida está un nivel por debajo de Sariya, use `GetAncestor(1)` como se muestra en el código siguiente:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    Esta vez el resultado solo muestra a Wanida.  
  
3.  Ahora cambie `@CurrentEmployee` a David (EmployeeID 6) y el nivel a 2. Ejecute lo siguiente para que también devuelva a Wanida:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    Esta vez, recibe también a Mary que también notifica a David, dos niveles más abajo.  
  
### <a name="to-use-getroot-and-getlevel"></a>Para usar GetRoot y GetLevel  
  
1.  A medida que la jerarquía crece, es más difícil determinar el lugar que ocupan los miembros en la jerarquía. Use el método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para buscar cuántos niveles existen bajo cada fila de la jerarquía. Ejecute el código siguiente para ver los niveles de todas las filas:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Use el método [GetRoot](../../t-sql/data-types/getroot-database-engine.md) para buscar el nodo raíz en la jerarquía. El código siguiente devuelve la fila única que es la raíz:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
La tarea siguiente reorganizará la jerarquía.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Reordenar los datos de una tabla jerárquica mediante métodos jerárquicos](../../relational-databases/tables/lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
  

