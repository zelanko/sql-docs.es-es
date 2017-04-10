---
title: "Lecci&#243;n 1: Convertir una tabla en una estructura jer&#225;rquica | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "HierarchyID"
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lecci&#243;n 1: Convertir una tabla en una estructura jer&#225;rquica
Los clientes que tienen tablas que utilizan autocombinaciones para expresar las relaciones jerárquicas pueden convertir sus tablas en una estructura jerárquica usando esta lección como guía. Es relativamente fácil migrar de esta representación a una que use **hierarchyid**. Después de la migración, los usuarios tendrán una representación jerárquica compacta y fácil de entender, que se puede indizar de varias maneras para conseguir consultas eficaces.  
  
En esta lección se examina una tabla existente, se crea una nueva tabla que contiene una columna **hierarchyid** , se rellena la tabla con los datos de la tabla de origen y, a continuación, se muestran tres estrategias de indización. En esta lección se incluyen los temas siguientes:  
  
-   [Examen de la estructura actual de la tabla Empleado](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
-   [Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Optimizar la tabla NewOrg](../../relational-databases/tables/optimizing-the-neworg-table.md)  
  
-   [Resumen: Conversión de una tabla en una estructura jerárquica](../../relational-databases/tables/summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## Requisitos previos  
Esta lección requiere la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
## Siguiente tarea de la lección  
[Examen de la estructura actual de la tabla Empleado](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
## Lección siguiente  
[Lección 2: Crear y administrar los datos de una tabla jerárquica](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
