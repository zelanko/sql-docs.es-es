---
title: Relleno de una tabla jerárquica usando métodos jerárquicos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c513aa5fb2c1f42b0eb2fa6c82deaac96c49d3ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112418"
---
# <a name="populating-a-hierarchical-table-using-hierarchical-methods"></a>Rellenar una tabla jerárquica usando métodos jerárquicos
  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tiene 8 empleados que trabajan en el departamento de marketing. La jerarquía de empleados ofrece el siguiente aspecto:  
  
 **David**, **EmployeeID** 6, es el jefe de marketing. Tres especialistas en marketing notifican a **David**:  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
 La asistente de marketing **Wanida** (**id. de empleado** 269) notifica a **Sariya**, mientras que la asistente de marketing **Mary** (**id. de empleado** 272) notifica a **John**.  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>Para insertar la raíz del árbol de jerarquía  
  
1.  El ejemplo siguiente inserta a **David** , jefe de marketing, en la raíz de la jerarquía dentro de la tabla. La columna **OrdLevel** es una columna calculada. Por lo tanto, no forma parte de la instrucción INSERT. Este primer registro usa el método [GetRoot()](/sql/t-sql/data-types/getroot-database-engine) para que se rellene este primer registro como la raíz de la jerarquía.  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Ejecute el código siguiente para examinar la fila inicial de la tabla:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
 Al igual que en la lección anterior, se usa el método `ToString()` para convertir el tipo de datos de `hierarchyid` en un formato más comprensible.  
  
### <a name="to-insert-a-subordinate-employee"></a>Para insertar a un empleado subordinado  
  
1.  **Sariya** notifica a **David**. Para insertar **Sariya** nodo, debe crear un adecuado **OrgNode** valor de tipo de datos `hierarchyid`. El código siguiente crea una variable de tipo de datos de `hierarchyid` y lo rellena con el valor raíz OrgNode de la tabla. Después, usa esa variable con el método [GetDescendant()](/sql/t-sql/data-types/getdescendant-database-engine) para insertar una fila que es un nodo subordinado. `GetDescendant` toma dos argumentos. Revise las opciones siguientes de los valores de argumento:  
  
    -   Si el elemento primario es NULL, `GetDescendant` devolverá NULL.  
  
    -   Si el elemento primario no es NULL y child1 y child2 son NULL, `GetDescendant` devuelve un elemento secundario del elemento primario.  
  
    -   Si el elemento primario y child1 no son NULL y, a su vez, child2 es NULL, `GetDescendant` devuelve un elemento secundario del elemento primario mayor que child1.  
  
    -   Si el elemento primario y child2 no son NULL y, a su vez, child1 es NULL, `GetDescendant` devuelve un elemento secundario del elemento primario menor que child2.  
  
    -   Si el elemento primario, child1 y child2 no son NULL, `GetDescendant` devuelve un elemento secundario del elemento primario mayor que child1 y menor que child2.  
  
     El código siguiente utiliza los argumentos `(NULL, NULL)` de la raíz primaria porque todavía no hay filas en la tabla (excepto la raíz). Ejecute el código siguiente para insertar a **Sariya**:  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Repita la consulta realizada con el primer procedimiento para consultar la tabla y ver cómo aparecen las entradas:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>Para crear un procedimiento que sirva para escribir nuevos nodos  
  
1.  Para simplificar la entrada de datos, cree el siguiente procedimiento almacenado a fin de agregar empleados a la tabla **EmployeeOrg** . El procedimiento acepta valores de entrada sobre el empleado que se está agregando. Este proceso contiene el **EmployeeID** del jefe del nuevo empleado, el número de **EmployeeID** del nuevo empleado, así como su nombre y puesto. El procedimiento usa `GetDescendant()` y también el método [GetAncestor()](/sql/t-sql/data-types/getancestor-database-engine) . Ejecute el código siguiente para crear el procedimiento:  
  
    ```  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  El ejemplo siguiente agrega los 4 empleados restantes que notifican directa o indirectamente a **David**.  
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Vuelva a ejecutar la consulta siguiente y examine las filas de la tabla **EmployeeOrg** :  
  
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
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
 La tabla estará totalmente rellena con la organización del departamento de marketing.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Realizar una consulta a una tabla jerárquica mediante métodos de jerarquía](lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
