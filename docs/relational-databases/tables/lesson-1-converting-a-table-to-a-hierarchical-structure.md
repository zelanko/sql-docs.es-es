---
title: 'Lección 1: Conversión de una tabla en una estructura jerárquica | Microsoft Docs'
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14b490c48cf60c01efa1a0c3fed38b4aabb10495
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716303"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lección 1: Conversión de una tabla en una estructura jerárquica
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Los clientes que tienen tablas que utilizan autocombinaciones para expresar las relaciones jerárquicas pueden convertir sus tablas en una estructura jerárquica usando esta lección como guía. Es relativamente fácil migrar de esta representación a una que use **hierarchyid**. Después de la migración, los usuarios tendrán una representación jerárquica compacta y fácil de entender, que se puede indizar de varias maneras para conseguir consultas eficaces.  
  
En esta lección se examina una tabla existente, se crea una nueva tabla que contiene una columna **hierarchyid** , se rellena la tabla con los datos de la tabla de origen y, a continuación, se muestran tres estrategias de indización. En esta lección se incluyen los temas siguientes:  
 
  
## <a name="prerequisites"></a>Prerequisites  
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor que ejecute SQL Server y una base de datos de AdventureWorks.

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargue las [bases de datos de ejemplo de AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Aquí encontrará instrucciones para restaurar bases de datos en SSMS: [Restaurar una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  

## <a name="examine-the-current-structure-of-the-employee-table"></a>Examen de la estructura actual de la tabla Employee
La base de datos de ejemplo Adventureworks2017 (o posterior) contiene una tabla llamada **Employee** (Empleado) en el esquema **HumanResources** (Recursos humanos). Para evitar cambiar la tabla original, este paso realiza una copia de la tabla **Employee** denominada **EmployeeDemo**. Para simplificar el ejemplo, copie solo cinco columnas de la tabla original. A continuación, consulte la tabla **HumanResources.EmployeeDemo** para examinar cómo los datos se estructuran en una tabla sin utilizar el tipo de datos **hierarchyid** .  
  
### <a name="copy-the-employee-table"></a>Copia de la tabla Employee  
  
1.  En una ventana del editor de consultas, ejecute el código siguiente para copiar la estructura y los datos de la tabla **Employee** en una nueva tabla denominada **EmployeeDemo**. Dado que la tabla original ya usa hierarchyid, esta consulta básicamente acopla la jerarquía para recuperar el administrador del empleado. En las siguientes partes de esta lección reconstruiremos esta jerarquía.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]


   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>Examen de la estructura y los datos de la tabla EmployeeDemo  
  
-   Esta nueva tabla **EmployeeDemo** representa una tabla típica en una base de datos existente que podría desear migrar a una nueva estructura. En una ventana del editor de consultas, ejecute el código siguiente para mostrar cómo la tabla utiliza una autocombinación para mostrar las relaciones empleado/administrador:  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    Los resultados continúan hasta un total de 290 filas.  
  
Observe que la cláusula **ORDER BY** hace que la lista de salida muestre juntos los informes directos de cada nivel de administración. Por ejemplo, los siete informes directos de **MgrID** 1 (ken0) aparecen agrupados. Aunque no imposible, es mucho más difícil de agrupar a todos aquellos que crean informes para **MgrID** 1.  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>Relleno de una tabla con los datos jerárquicos existentes
Esta tarea crea una nueva tabla y la rellena con los datos de la tabla **EmployeeDemo** . Esta tarea consta de los pasos siguientes:  
  
-   Cree una nueva tabla que contenga una columna **hierarchyid** . Esta columna podría reemplazar a las columnas **EmployeeID** y **ManagerID** existentes. Sin embargo, usted conservará esas columnas. La razón de ello es porque alguna de las aplicaciones existentes podría hacer referencia a esas columnas, y también para ayudarle a entender los datos una vez realizada la transferencia. La definición de tabla especifica que **OrgNode** es la clave principal, que requiere que la columna contenga valores únicos. El índice agrupado sobre la columna **OrgNode** almacenará la fecha en secuencia **OrgNode** .    
-   Cree una tabla temporal que se utilizará para averiguar cuántos empleados notifican directamente a cada gerente. 
-   Rellene la nueva tabla con los datos de la tabla **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Para crear una nueva tabla denominada NewOrg  
  
-   En una ventana del Editor de consultas, ejecute el siguiente código para crear una nueva tabla denominada **HumanResources.NewOrg**:  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="create-a-temporary-table-named-children"></a>Creación de una tabla temporal denominada #Elementos secundarios  
  
1.  Cree una tabla temporal denominada **#Elementos secundarios** con una columna denominada **Num** que contendrá el número de elementos secundarios de cada nodo:  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Agregue un índice que acelerará significativamente la consulta que rellena la tabla **NewOrg** :  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>Relleno de la tabla NewOrg  
  
1.  Las consultas recursivas prohíben las subconsultas con agregados. En su lugar, rellene la tabla **#Elementos secundarios** con el código siguiente, que usa el método [ROW_NUMBER ()](../../t-sql/functions/row-number-transact-sql.md) para rellenar la columna **Num** :  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  Revise la tabla **#Elementos secundarios** . Observe cómo la columna **Num** contiene números secuenciales para cada administrador.  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  Rellene la tabla **NewOrg** . Use los métodos GetRoot y ToString para concatenar los valores **Num** en formato **hierarchyid** y, después, actualice la columna **OrgNode** con los valores jerárquicos resultantes:  
  
    ```sql  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   

    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  Una columna **hierarchyid** se entiende mejor al convertirla al formato de caracteres. Revise los datos de la tabla **NewOrg** ; para ello, ejecute el código siguiente, que contiene dos representaciones de la columna **OrgNode** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    La columna **LogicalNode** convierte la columna **hierarchyid** en un texto más fácil de leer que representa la jerarquía. En las tareas restantes, usará el método `ToString()` para mostrar el formato lógico de las columnas **hierarchyid** .  
  
5.  Elimine la tabla temporal, que ya no se necesita:  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>Optimizar la tabla NewOrg
La tabla **NewOrd** que ha creado en la tarea [Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contiene toda la información del empleado y representa la estructura jerárquica mediante un tipo de datos **hierarchyid**. Esta tarea agrega los nuevos índices que admiten las búsquedas en la columna **hierarchyid** .  
  

La columna **hierarchyid** (**OrgNode**) es la clave principal de la tabla **NewOrg** . Al crear la tabla, contenía un índice agrupado denominado **PK_NewOrg_OrgNode** para exigir la singularidad de la columna **OrgNode** . Este índice clúster también admite una búsqueda con prioridad a la profundidad de la tabla.  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>Creación de un índice en la tabla NewOrg para realizar búsquedas eficaces  
  
1.  Si quiere ayudar a realizar consultas en el mismo nivel de la jerarquía, use el método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para crear una columna calculada que contenga el nivel en la jerarquía. Después cree un índice compuesto en el nivel y **Hierarchyid**. Ejecute el código siguiente para crear la columna calculada y el índice con prioridad a la amplitud:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Cree un índice único en la columna **EmployeeID** . Esta es la búsqueda singleton tradicional de un empleado único por número de **EmployeeID** . Ejecute el código siguiente para crear un índice en **EmployeeID**:  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Ejecute el código siguiente para recuperar los datos en la tabla en el orden de cada uno de los tres índices:  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Compare los conjuntos de resultados para ver cómo se almacena el orden en cada tipo de índice. Solo siguen las primeras cuatro filas de cada de salida.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    El índice con prioridad a la profundidad: los registros del empleado se almacenan junto a su administrador.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    El índice con prioridad a **EmployeeID**: las filas se almacenan en secuencia de **EmployeeID** .  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> Para diagramas que muestran la diferencia entre un índice con prioridad a la profundidad y uno con prioridad a la amplitud, consulte [Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
### <a name="drop-the-unnecessary-columns"></a>Eliminación de las columnas innecesarias  
  
1.  La columna **ManagerID** representa la relación de empleado/administrador, que representa ahora la columna **OrgNode** . Si el resto de aplicaciones no necesitan la columna **ManagerID** , considere la posibilidad de quitarla mediante la siguiente instrucción:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  La columna **EmployeeID** también es redundante. La columna **OrgNode** identifica singularmente a cada empleado. Si otras aplicaciones no necesitan la columna **EmployeeID** , considere la posibilidad de quitar el índice y, después, la columna mediante el código siguiente:  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>Sustitución de la tabla original por la nueva tabla  
  
1.  Si la tabla original contenía algún índice o restricción adicional, agréguelos a la tabla **NewOrg** .  
  
2.  Reemplace la antigua tabla **EmployeeDemo** por la nueva. Ejecute el código siguiente para quitar la tabla antigua y, a continuación, cambie el nombre de la nueva tabla con el nombre anterior:  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Ejecute el código siguiente para examinar la tabla final:  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se muestra cómo crear y administrar datos en una tabla jerárquica. 

Vaya al siguiente artículo para más información:
> [!div class="nextstepaction"]
> [Pasos siguientes](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)
