---
title: 'Lección 1: Conversión de una tabla en una estructura jerárquica | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
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
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a38cbcec7f42ff99e0e7c56de16fc30a3187dded
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042633"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lección 1: Convertir una tabla en una estructura jerárquica
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Los clientes que tienen tablas que utilizan autocombinaciones para expresar las relaciones jerárquicas pueden convertir sus tablas en una estructura jerárquica usando esta lección como guía. Es relativamente fácil migrar de esta representación a una que use **hierarchyid**. Después de la migración, los usuarios tendrán una representación jerárquica compacta y fácil de entender, que se puede indizar de varias maneras para conseguir consultas eficaces.  
  
En esta lección se examina una tabla existente, se crea una nueva tabla que contiene una columna **hierarchyid** , se rellena la tabla con los datos de la tabla de origen y, a continuación, se muestran tres estrategias de indización. En esta lección se incluyen los temas siguientes:  
  
-   [Examen de la estructura actual de la tabla Empleado](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Optimizar la tabla NewOrg](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [Resumen: Conversión de una tabla en una estructura jerárquica](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>Prerequisites  
Esta lección requiere la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Examen de la estructura actual de la tabla Empleado](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Creación y administración de los datos de una tabla jerárquica](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
