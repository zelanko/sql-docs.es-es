---
title: Realización de una consulta a una tabla jerárquica mediante métodos de jerarquía | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be1d0dcd37dba9b1025ba3e4a93aa60d2198b237
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110045"
---
# <a name="querying-a-hierarchical-table-using-hierarchy-methods"></a>Realizar una consulta a una tabla jerárquica mediante métodos de jerarquía
  Ahora que está totalmente rellena la tabla HumanResources.EmployeeOrg, esta tarea mostrará cómo realizar una consulta en la jerarquía utilizando alguno de los métodos jerárquicos.  
  
### <a name="to-find-subordinate-nodes"></a>Para buscar nodos subordinados  
  
1.  Sariya tiene un empleado subordinado. Para consultar los subordinados de Sariya, ejecute la consulta siguiente que usa el método [IsDescendantOf](/sql/t-sql/data-types/isdescendantof-database-engine) :  
  
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
  
2.  También se puede consultar esta información mediante el método [GetAncestor](/sql/t-sql/data-types/getancestor-database-engine) . `GetAncestor` toma un argumento para el nivel que está intentando devolver. Puesto que Wanida está un nivel por debajo de Sariya, use `GetAncestor(1)` como se muestra en el código siguiente:  
  
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
  
1.  A medida que la jerarquía crece, es más difícil determinar el lugar que ocupan los miembros en la jerarquía. Use el método [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) para buscar cuántos niveles existen bajo cada fila de la jerarquía. Ejecute el código siguiente para ver los niveles de todas las filas:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Use el método [GetRoot](/sql/t-sql/data-types/getroot-database-engine) para buscar el nodo raíz en la jerarquía. El código siguiente devuelve la fila única que es la raíz:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
 La tarea siguiente reorganizará la jerarquía.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Reordenar los datos de una tabla jerárquica mediante métodos jerárquicos](lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
