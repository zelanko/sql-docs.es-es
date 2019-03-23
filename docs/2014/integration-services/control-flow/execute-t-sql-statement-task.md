---
title: Tarea Ejecutar instrucción T-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f20f64c9a26d1e9b030c01618a63157757c0b205
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375483"
---
# <a name="execute-t-sql-statement-task"></a>Tarea Ejecutar instrucción T-SQL
  La tarea Ejecutar instrucción T-SQL ejecuta instrucciones Transact-SQL. Para más información, vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) y [Consultas de Integration Services &#40;SSIS&#41;](../integration-services-ssis-queries.md).  
  
 Esta tarea es similar a la tarea Ejecutar SQL. Sin embargo, la tarea Ejecutar instrucción T-SQL solo admite la versión Transact-SQL del lenguaje SQL, por lo que no se puede usar esta tarea para ejecutar instrucciones en servidores que usen otros dialectos del lenguaje SQL. Si necesita ejecutar consultas con parámetros, guardar los resultados de la consulta en variables o usar expresiones de propiedades, debe usar la tarea Ejecutar SQL en lugar de la tarea Ejecutar instrucción T-SQL. Para más información, consulte [Execute SQL Task](execute-sql-task.md).  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>Configuración de la tarea Ejecutar T-SQL  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Ejecutar instrucción T-SQL &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)   
 [MERGE en paquetes de Integration Services](merge-in-integration-services-packages.md)  
  
  
