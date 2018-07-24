---
title: Examen de la estructura actual de la tabla Employee | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 620defd42e27b122a92ee145da6b4b14d1cbf996
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970307"
---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>Lección 1-1: Examen de la estructura actual de la tabla Employee
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
La base de datos de ejemplo de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] (o posterior) contiene una tabla llamada **Employee** (Empleado) en el esquema **HumanResources** (Recursos humanos). Para evitar cambiar la tabla original, este paso realiza una copia de la tabla **Employee** denominada **EmployeeDemo**. Para simplificar el ejemplo, copie solo cinco columnas de la tabla original. A continuación, consulte la tabla **HumanResources.EmployeeDemo** para examinar cómo los datos se estructuran en una tabla sin utilizar el tipo de datos **hierarchyid** .  
  
### <a name="to-copy-the-employee-table"></a>Para copiar la tabla Employee  
  
1.  En una ventana del editor de consultas, ejecute el código siguiente para copiar la estructura y los datos de la tabla **Employee** en una nueva tabla denominada **EmployeeDemo**. Dado que la tabla original ya usa hierarchyid, esta consulta básicamente acopla la jerarquía para recuperar el administrador del empleado. En las siguientes partes de esta lección reconstruiremos esta jerarquía.
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
      (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
            WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
                (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID
        , emp.JobTitle, emp.HireDate
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee emp ;
    GO
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>Para examinar la estructura y los datos de la tabla EmployeeDemo  
  
-   Esta nueva tabla **EmployeeDemo** representa una tabla típica en una base de datos existente que podría desear migrar a una nueva estructura. En una ventana del editor de consultas, ejecute el código siguiente para mostrar cómo la tabla utiliza una autocombinación para mostrar las relaciones empleado/administrador:  
  
    ```  
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
    NULL    NULL    1   adventure-works\ken0    Chief Executive Officer
    1   adventure-works\ken0    2   adventure-works\terri0  Vice President of Engineering
    1   adventure-works\ken0    16  adventure-works\david0  Marketing Manager
    1   adventure-works\ken0    25  adventure-works\james1  Vice President of Production
    1   adventure-works\ken0    234 adventure-works\laura1  Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0   Information Services Manager
    1   adventure-works\ken0    273 adventure-works\brian3  Vice President of Sales
    2   adventure-works\terri0  3   adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0    Senior Tool Designer
    ...  
    ```  
  
    Los resultados continúan hasta un total de 290 filas.  
  
Observe que la cláusula **ORDER BY** hace que la lista de salida muestre juntos los informes directos de cada nivel de administración. Por ejemplo, los siete informes directos de **MgrID** 1 (ken0) aparecen agrupados. Aunque no imposible, es mucho más difícil de agrupar a todos aquellos que crean informes para **MgrID** 1.  
  
En la tarea siguiente, crearemos una nueva tabla con un tipo de datos **hierarchyid** y pasaremos los datos a la nueva tabla.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  
