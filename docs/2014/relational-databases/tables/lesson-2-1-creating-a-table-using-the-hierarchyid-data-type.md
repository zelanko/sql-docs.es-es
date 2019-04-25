---
title: Creación de una tabla mediante el tipo de datos hierarchyid | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 0d1f361f-336c-4571-99d1-f4813b2d9fc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5af072e27ff1e1c70d6a3035ceb7eb2a1cc2493
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760908"
---
# <a name="creating-a-table-using-the-hierarchyid-data-type"></a>Crear una tabla mediante el tipo de datos hierarchyid
  El ejemplo siguiente crea una tabla denominada EmployeeOrg que contiene los datos del empleado y la jerarquía correspondiente. El ejemplo crea la tabla en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , aunque esta ubicación es opcional. Para mantener un esquema sencillo del ejemplo, esta tabla solo incluye cinco columnas:  
  
-   OrgNode es una columna `hierarchyid` que almacena la relación jerárquica.  
  
-   OrgLevel es una columna calculada que se basa en la columna OrgNode y que almacena todos los niveles de nodos de la jerarquía. Se usará para crear un índice con prioridad a la amplitud.  
  
-   EmployeeID contiene el número de identificación típico del empleado que se utiliza para aplicaciones como, por ejemplo, la nómina. En el nuevo desarrollo de aplicaciones, las aplicaciones pueden utilizar la columna OrgNode y la columna EmployeeID independiente no es necesaria.  
  
-   EmpName contiene el nombre del empleado.  
  
-   Title contiene el puesto del empleado.  
  
### <a name="to-create-the-employeeorg-table"></a>Para crear la tabla EmployeeOrg  
  
1.  En una ventana del Editor de consultas, ejecute el código siguiente para crear la tabla `EmployeeOrg` . Al especificar la columna `OrgNode` como la clave principal con un índice clúster, se creará un índice con prioridad a la profundidad:  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
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
  
    ```  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
 Ahora ya puede usar la tabla para trabajar con datos. La siguiente tarea rellenará la tabla mediante métodos jerárquicos.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Rellenar una tabla jerárquica usando métodos jerárquicos](lesson-2-2-populating-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
