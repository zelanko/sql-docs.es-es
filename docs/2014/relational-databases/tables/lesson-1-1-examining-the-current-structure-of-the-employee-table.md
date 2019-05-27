---
title: Examen de la estructura actual de la tabla Employee | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b88c78a1a7f4244afe220585919a50ed06cd0ad9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66110139"
---
# <a name="examining-the-current-structure-of-the-employee-table"></a>Examen de la estructura actual de la tabla Empleado
  La base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] contiene una tabla llamada **Employee** en el esquema **HumanResources** . Para evitar cambiar la tabla original, este paso realiza una copia de la tabla **Employee** denominada **EmployeeDemo**. Para simplificar el ejemplo, copie solo cinco columnas de la tabla original. A continuación, consulte el **HumanResources.EmployeeDemo** tabla para revisar cómo se estructuran los datos en una tabla sin utilizar el `hierarchyid` tipo de datos.  
  
### <a name="to-copy-the-employee-table"></a>Para copiar la tabla Employee  
  
1.  En una ventana del editor de consultas, ejecute el código siguiente para copiar la estructura y los datos de la tabla **Employee** en una nueva tabla denominada **EmployeeDemo**.  
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT EmployeeID, LoginID, ManagerID, Title, HireDate   
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee ;  
    GO  
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>Para examinar la estructura y los datos de la tabla EmployeeDemo  
  
-   Esta nueva tabla **EmployeeDemo** representa una tabla típica en una base de datos existente que podría desear migrar a una nueva estructura. En una ventana del editor de consultas, ejecute el código siguiente para mostrar cómo la tabla utiliza una autocombinación para mostrar las relaciones empleado/administrador:  
  
    ```  
    SELECT   
         Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
         Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.Title  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  Title  
    NULL NULL                      109 adventure-works\ken0     Chief Executive Officer  
    3    adventure-works\roberto0  4   adventure-works\rob0     Senior Tool Designer  
    3    adventure-works\roberto0  9   adventure-works\gail0    Design Engineer  
    3    adventure-works\roberto0  11  adventure-works\jossef0  Design Engineer  
    3    adventure-works\roberto0  158 adventure-works\dylan0   Research and Development Manager  
    3    adventure-works\roberto0  263 adventure-works\ovidiu0  Senior Tool Designer  
    3    adventure-works\roberto0  267 adventure-works\michael8 Senior Design Engineer  
    3    adventure-works\roberto0  270 adventure-works\sharon0  Design Engineer  
    6    adventure-works\david0    2   adventure-works\kevin0   Marketing Assistant  
    ...  
    ```  
  
     Los resultados continúan hasta un total de 290 filas.  
  
 Observe que la cláusula `ORDER BY` hace que la lista de salida muestre juntos los informes directos de cada nivel de administración. Por ejemplo, los siete informes directos de **MgrID** 3 (roberto0) aparecen agrupados. Aunque no imposible, es mucho más difícil de agrupar a todos aquellos que crean informes para **MgrID** 3.  
  
 En la tarea siguiente, crearemos una nueva tabla con un tipo de datos `hierarchyid` y pasaremos los datos a la nueva tabla.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Rellenar una tabla con los datos jerárquicos existentes](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
