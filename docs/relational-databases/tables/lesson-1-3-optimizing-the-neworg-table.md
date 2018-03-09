---
title: "Optimización de la tabla NewOrg | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2526b0a159349655b68f6364e6a070e4661e422
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>Lección 1-3: Optimizar la tabla NewOrg
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] La tabla **NewOrd** que ha creado en la tarea [Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contiene toda la información del empleado y representa la estructura jerárquica mediante un tipo de datos **hierarchyid**. Esta tarea agrega los nuevos índices que admiten las búsquedas en la columna **hierarchyid** .  
  
## <a name="clustered-index"></a>Índice agrupado  
La columna **hierarchyid** (**OrgNode**) es la clave principal de la tabla **NewOrg** . Al crear la tabla, contenía un índice agrupado denominado **PK_NewOrg_OrgNode** para exigir la singularidad de la columna **OrgNode** . Este índice clúster también admite una búsqueda con prioridad a la profundidad de la tabla.  
  
## <a name="nonclustered-index"></a>Índice no agrupado  
Este paso crea dos índices no clúster que admiten búsquedas típicas.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>Para indizar la tabla NewOrg a fin de realizar búsquedas eficaces  
  
1.  Si quiere ayudar a realizar consultas en el mismo nivel de la jerarquía, use el método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para crear una columna calculada que contenga el nivel en la jerarquía. Después cree un índice compuesto en el nivel y **Hierarchyid**. Ejecute el código siguiente para crear la columna calculada y el índice con prioridad a la amplitud:  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Cree un índice único en la columna **EmployeeID** . Esta es la búsqueda singleton tradicional de un empleado único por número de **EmployeeID** . Ejecute el código siguiente para crear un índice en **EmployeeID**:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  Ejecute el código siguiente para recuperar los datos en la tabla en el orden de cada uno de los tres índices:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Compare los conjuntos de resultados para ver cómo se almacena el orden en cada tipo de índice. Solo siguen las primeras cuatro filas de cada de salida.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Índice con prioridad a la profundidad: los registros del empleado se almacenan junto a su administrador.  
  
    `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
    `/             0x         0         1      zarifin`  
  
    `/1/          0x58        1         2      tplate`  
  
    `/1/1/       0x5AC0       2         4      schai`  
  
    `/1/1/1/     0x5AD6       3         9      jwang`  
  
    `/1/1/2/     0x5ADA       3        10      malexander`  
  
    `/1/2/       0x5B40       2         5      elang`  
  
    `/1/3/       0x5BC0       2         6      gsmits`  
  
    `/2/         0x68         1         3      hjensen`  
  
    `/2/1/       0x6AC0       2         7      sdavis`  
  
    `/2/2/       0x6B40       2         8      norint`  
  
    El índice con prioridad a **EmployeeID**: las filas se almacenan en secuencia de **EmployeeID**.  
  
    `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
    `/             0x         0         1      zarifin`  
  
    `/1/          0x58        1         2      tplate`  
  
    `/2/         0x68         1         3      hjensen`  
  
    `/1/1/       0x5AC0       2         4      schai`  
  
    `/1/2/       0x5B40       2         5      elang`  
  
    `/1/3/       0x5BC0       2         6      gsmits`  
  
    `/2/1/       0x6AC0       2         7      sdavis`  
  
    `/2/2/       0x6B40       2         8      norint`  
  
    `/1/1/1/     0x5AD6       3         9      jwang`  
  
    `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
> Para diagramas que muestran la diferencia entre un índice con prioridad a la profundidad y uno con prioridad a la amplitud, consulte [Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>Para eliminar las columnas innecesarias  
  
1.  La columna **ManagerID** representa la relación de empleado/administrador, que representa ahora la columna **OrgNode** . Si el resto de aplicaciones no necesitan la columna **ManagerID** , considere la posibilidad de quitarla mediante la siguiente instrucción:  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  La columna **EmployeeID** también es redundante. La columna **OrgNode** identifica singularmente a cada empleado. Si otras aplicaciones no necesitan la columna **EmployeeID** , considere la posibilidad de quitar el índice y, después, la columna mediante el código siguiente:  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>Para sustituir la tabla original por la nueva tabla  
  
1.  Si la tabla original contenía algún índice o restricción adicional, agréguelos a la tabla **NewOrg** .  
  
2.  Reemplace la antigua tabla **EmployeeDemo** por la nueva. Ejecute el código siguiente para quitar la tabla antigua y, a continuación, cambie el nombre de la nueva tabla con el nombre anterior:  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  Ejecute el código siguiente para examinar la tabla final:  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Resumen: Conversión de una tabla en una estructura jerárquica](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  
