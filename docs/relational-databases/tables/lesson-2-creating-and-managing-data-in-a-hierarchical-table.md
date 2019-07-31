---
title: 'Lección 2: Creación y administración de los datos de una tabla jerárquica | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 657dedcf4944a2540d1237b53fa8ea822c31ae3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031645"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>Lección 2: Creación y administración de los datos de una tabla jerárquica
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
En la lección 1, ha modificado una tabla existente para usar el tipo de datos **hierarchyid** y ha rellenado la columna **hierarchyid** con la representación de los datos existentes. En esta lección, se iniciará con una nueva tabla e insertará los datos utilizando los métodos jerárquicos. A continuación, se consultarán y manipularán los datos utilizando los métodos jerárquicos. 

## <a name="prerequisites"></a>Prerequisites  
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor que ejecute SQL Server y una base de datos de AdventureWorks.

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargue las [bases de datos de ejemplo de AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Aquí encontrará instrucciones para restaurar bases de datos en SSMS: [Restaurar una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>Creación de una tabla mediante el tipo de datos hierarchyid
El ejemplo siguiente crea una tabla denominada EmployeeOrg que contiene los datos del empleado y la jerarquía correspondiente. En el ejemplo se crea la tabla en la base de datos AdventureWorks2017, aunque es opcional. Para mantener un esquema sencillo del ejemplo, esta tabla solo incluye cinco columnas:  
  
-   OrgNode es una columna **hierarchyid** que almacena la relación jerárquica.   
-   OrgLevel es una columna calculada que se basa en la columna OrgNode y que almacena todos los niveles de nodos de la jerarquía. Se usará para crear un índice con prioridad a la amplitud.  
-   EmployeeID contiene el número de identificación típico del empleado que se utiliza para aplicaciones como, por ejemplo, la nómina. En el nuevo desarrollo de aplicaciones, las aplicaciones pueden utilizar la columna OrgNode y la columna EmployeeID independiente no es necesaria.   
-   EmpName contiene el nombre del empleado.    
-   Title contiene el puesto del empleado.  

## <a name="create-the-employeeorg-table"></a>Creación de la tabla EmployeeOrg  
  
1.  En una ventana del Editor de consultas, ejecute el código siguiente para crear la tabla `EmployeeOrg` . Al especificar la columna `OrgNode` como la clave principal con un índice clúster, se creará un índice con prioridad a la profundidad:  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  Ejecute el código siguiente para crear un índice compuesto en las columnas `OrgLevel` y `OrgNode` que admita búsquedas eficaces con prioridad a la amplitud:  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
Ahora ya puede usar la tabla para trabajar con datos. La siguiente tarea rellenará la tabla mediante métodos jerárquicos.   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>Relleno de una tabla jerárquica mediante métodos jerárquicos
AdventureWorks2017 tiene ocho empleados que trabajan en el departamento de marketing. La jerarquía de empleados ofrece el siguiente aspecto:  
  
**David**, **EmployeeID** 6, es el jefe de marketing. Tres especialistas en marketing notifican a **David**:  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
La asistente de marketing **Wanida** (**id. de empleado** 269) notifica a **Sariya**, mientras que la asistente de marketing **Mary** (**id. de empleado** 272) notifica a **John**.  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>Inserción de la raíz del árbol de jerarquía  
  
1.  El ejemplo siguiente inserta a **David** , jefe de marketing, en la raíz de la jerarquía dentro de la tabla. La columna **OrdLevel** es una columna calculada. Por lo tanto, no forma parte de la instrucción INSERT. Este primer registro usa el método [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) para que se rellene este primer registro como la raíz de la jerarquía.  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Ejecute el código siguiente para examinar la fila inicial de la tabla:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
Al igual que en la lección anterior, se usa el método `ToString()` para convertir el tipo de datos **hierarchyid** en un formato más comprensible.  
  
### <a name="insert-a-subordinate-employee"></a>Inserción de un empleado subordinado  
  
1.  **Sariya** notifica a **David**. Para insertar el nodo de **Sariya** , debe crear un valor **OrgNode** adecuado del tipo de datos de **hierarchyid**. El código siguiente crea una variable de tipo de datos de **hierarchyid** y lo rellena con el valor raíz OrgNode de la tabla. Después, usa esa variable con el método [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) para insertar una fila que es un nodo subordinado. `GetDescendant` toma dos argumentos. Revise las opciones siguientes de los valores de argumento:  
  
    -   Si el elemento primario es NULL, `GetDescendant` devolverá NULL.  
    -   Si el elemento primario no es NULL y child1 y child2 son NULL, `GetDescendant` devuelve un elemento secundario del elemento primario.  
    -   Si el elemento primario y child1 no son NULL y, a su vez, child2 es NULL, `GetDescendant` devuelve un elemento secundario del elemento primario mayor que child1.   
    -   Si el elemento primario y child2 no son NULL y, a su vez, child1 es NULL, `GetDescendant` devuelve un elemento secundario del elemento primario menor que child2.   
    -   Si el elemento primario, child1 y child2 no son NULL, `GetDescendant` devuelve un elemento secundario del elemento primario mayor que child1 y menor que child2.  
  
    El código siguiente utiliza los argumentos `(NULL, NULL)` de la raíz primaria porque todavía no hay filas en la tabla (excepto la raíz). Ejecute el código siguiente para insertar a **Sariya**:  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Repita la consulta realizada con el primer procedimiento para consultar la tabla y ver cómo aparecen las entradas:  
  
    ```sql  
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
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>Creación de un procedimiento para escribir nuevos nodos  
  
1.  Para simplificar la entrada de datos, cree el siguiente procedimiento almacenado a fin de agregar empleados a la tabla **EmployeeOrg** . El procedimiento acepta valores de entrada sobre el empleado que se está agregando. Este proceso contiene el **EmployeeID** del jefe del nuevo empleado, el número de **EmployeeID** del nuevo empleado, así como su nombre y puesto. El procedimiento usa `GetDescendant()` y también el método [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) . Ejecute el código siguiente para crear el procedimiento:  
  
    ```sql  
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
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Vuelva a ejecutar la consulta siguiente y examine las filas de la tabla **EmployeeOrg** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
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

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>Consultar una tabla jerárquica mediante métodos de jerarquía
Ahora que está totalmente rellena la tabla HumanResources.EmployeeOrg, esta tarea mostrará cómo realizar una consulta en la jerarquía utilizando alguno de los métodos jerárquicos.  
  
### <a name="find-subordinate-nodes"></a>Búsqueda de nodos subordinados  
  
1.  Sariya tiene un empleado subordinado. Para consultar los subordinados de Sariya, ejecute la consulta siguiente que usa el método [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) :  
  
    ```sql  
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
  
    ```sql  
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
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    Esta vez, recibe también a Mary que también notifica a David, dos niveles más abajo.  
  
## <a name="use-getroot-and-getlevel"></a>Uso de GetRoot y GetLevel  
  
1.  A medida que la jerarquía crece, es más difícil determinar el lugar que ocupan los miembros en la jerarquía. Use el método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para buscar cuántos niveles existen bajo cada fila de la jerarquía. Ejecute el código siguiente para ver los niveles de todas las filas:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Use el método [GetRoot](../../t-sql/data-types/getroot-database-engine.md) para buscar el nodo raíz en la jerarquía. El código siguiente devuelve la fila única que es la raíz:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>Reordenación de los datos de una tabla jerárquica mediante métodos jerárquicos
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Reorganizar una jerarquía es una tarea de mantenimiento común. En esta tarea, usaremos una instrucción UPDATE con el método [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) para mover primero una única fila a una nueva ubicación en la jerarquía. A continuación, moveremos un subárbol completo a una nueva ubicación.  
  
El método `GetReparentedValue` tiene dos argumentos. El primer argumento describe la parte de la jerarquía que se va a modificar. Por ejemplo, si una jerarquía es **/1/4/2/3/** y quiere cambiar la sección **/1/4/** , la jerarquía se vuelve **/2/1/2/3/** , dejando los dos últimos nodos (**2/3/** ) sin modificar. Debe proporcionar los nodos que cambian ( **/1/4/** ) como el primer argumento. El segundo argumento proporciona el nuevo nivel de jerarquía; en nuestro ejemplo, **/2/1/** . No es necesario que los dos argumentos tengan el mismo número de niveles.  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>Desplazamiento de una fila a una ubicación nueva en la jerarquía  
  
1.  Actualmente Wanida notifica a Sariya. En este procedimiento, se mueve a Wanida de su nodo actual **/1/1/,** de modo que notificará a Jill. Su nuevo nodo se volverá **/3/1/** , por lo que **/1/** es el primer argumento y **/3/** el segundo. Estos se corresponden con los valores **OrgNode** de Sariya y Jill. Ejecute el código siguiente para mover a Wanida de la organización de Sariya a la de Jill:  
  
    ```sql  
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
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    Wanida está ahora en el nodo **/3/1/** .  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>Reorganización de una sección de una jerarquía  
  
1.  Para mostrar cómo mover al mismo tiempo un gran número de personas, ejecute primero el código siguiente para agregar un becario a cargo de Wanida:  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Ahora Kevin notifica a Wanida, quien notifica a Jill, quien, a su vez, notifica a David. Eso quiere decir que Kevin está en el nivel **/3/1/1/** . Para mover todos los subordinados de Jill a un nuevo administrador, vamos a actualizar a un nuevo valor todos los nodos que tienen **/3/** como **OrgNode** . Ejecute el código siguiente para actualizar a Wanida de manera que dependa de Sariya, pero dejando que Kevin dependa de Wanida:  
  
    ```sql  
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
  
    ```sql  
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
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
El árbol completo de la organización que había notificado a Jill (tanto Wanida como Kevin) ahora notifica a Sariya.  
  
Para conseguir un procedimiento almacenado que reorganice una sección de una jerarquía, consulte la sección "Mover los subárboles" de [Mover los subárboles](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees).  
  
