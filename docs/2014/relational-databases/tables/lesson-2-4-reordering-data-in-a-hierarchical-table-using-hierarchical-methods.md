---
title: Reordenación de los datos de una tabla jerárquica mediante métodos jerárquicos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 7b8064c7-62c6-488d-84d2-57a5828fb907
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c53303d238db802c6da2d1ec5e443fcff503bec8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208665"
---
# <a name="reordering-data-in-a-hierarchical-table-using-hierarchical-methods"></a>Reordenar los datos de una tabla jerárquica mediante métodos jerárquicos
  Reorganizar una jerarquía es una tarea de mantenimiento común. En esta tarea, usaremos una instrucción UPDATE con el método [GetReparentedValue](/sql/t-sql/data-types/getreparentedvalue-database-engine) para mover primero una única fila a una nueva ubicación en la jerarquía. A continuación, moveremos un subárbol completo a una nueva ubicación.  
  
 El método `GetReparentedValue` tiene dos argumentos. El primer argumento describe la parte de la jerarquía que se va a modificar. Por ejemplo, si una jerarquía es **/1/4/2/3/** y quiere cambiar la sección **/1/4/** , la jerarquía se vuelve **/2/1/2/3/**, dejando los dos últimos nodos (**2/3/**) sin modificar. Debe proporcionar los nodos que cambian (**/1/4/**) como el primer argumento. El segundo argumento proporciona el nuevo nivel de jerarquía; en nuestro ejemplo, **/2/1/**. No es necesario que los dos argumentos tengan el mismo número de niveles.  
  
### <a name="to-move-a-single-row-to-a-new-location-in-the-hierarchy"></a>Para mover una fila única a una nueva ubicación en la jerarquía  
  
1.  Actualmente Wanida notifica a Sariya. En este procedimiento, se mueve a Wanida de su nodo actual **/1/1/,** de modo que notificará a Jill. Su nuevo nodo se volverá **/3/1/** , por lo que **/1/** es el primer argumento y **/3/** el segundo. Estos se corresponden con los valores **OrgNode** de Sariya y Jill. Ejecute el código siguiente para mover a Wanida de la organización de Sariya a la de Jill:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  Ejecute el código siguiente para ver el resultado:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
     Wanida está ahora en el nodo **/3/1/**.  
  
### <a name="to-reorganize-a-section-of-a-hierarchy"></a>Para reorganizar una sección de una jerarquía  
  
1.  Para mostrar cómo mover al mismo tiempo un gran número de personas, ejecute primero el código siguiente para agregar un becario a cargo de Wanida:  
  
    ```  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Ahora Kevin notifica a Wanida, quien notifica a Jill, quien, a su vez, notifica a David. Eso quiere decir que Kevin está en el nivel **/3/1/1/**. Para mover todos los subordinados de Jill a un nuevo administrador, vamos a actualizar a un nuevo valor todos los nodos que tienen **/3/** como **OrgNode** . Ejecute el código siguiente para actualizar a Wanida de manera que dependa de Sariya, pero dejando que Kevin dependa de Wanida:  
  
    ```  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  Ejecute el código siguiente para ver el resultado:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1//2      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
 El árbol completo de la organización que había notificado a Jill (tanto Wanida como Kevin) ahora notifica a Sariya.  
  
 Para conseguir un procedimiento almacenado que reorganice una sección de una jerarquía, consulte la sección "Mover los subárboles" de [Mover los subárboles](../hierarchical-data-sql-server.md#BKMK_MovingSubtrees).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Resumen: Administración de los datos de una tabla jerárquica](lesson-2-5-summary-managing-data-in-a-hierarchical-table.md)  
  
  
