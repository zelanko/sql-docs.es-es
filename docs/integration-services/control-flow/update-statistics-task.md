---
title: "Tarea Actualizar estadísticas | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
caps.latest.revision: "45"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: daae142be528b1918f7f77cab89650efd807cb40
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="update-statistics-task"></a>Tarea Actualizar estadísticas
  La tarea Actualizar estadísticas actualiza información sobre la distribución de valores clave para uno o varios grupos de estadísticas (colecciones) de la tabla o vista indizada especificada. Para obtener más información, vea [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Si utiliza la tarea Actualizar estadísticas, un paquete puede actualizar estadísticas para una o varias bases de datos. Si la tarea solo actualiza las estadísticas de una base de datos individual, puede elegir las vistas o las tablas para las que se van a actualizar las estadísticas. Puede configurar la actualización para que actualice todas las estadísticas, solo estadísticas de columnas o solo estadísticas de índices.  
  
 Esta tarea encapsula una instrucción UPDATE STATISTICS con los siguientes argumentos y cláusulas:  
  
-   El argumento *table_name* o *view_name* .  
  
-   Si se aplica la actualización a todas las estadísticas, la cláusula WITH ALL está implícita.  
  
-   Si la actualización solo se aplica a columnas, se incluye la cláusula WITH COLUMN.  
  
-   Si la actualización solo se aplica a índices, se incluye la cláusula WITH INDEX.  
  
 Si la tarea Actualizar estadísticas actualiza las estadísticas en varias bases de datos, la tarea ejecuta múltiples instrucciones UPDATE STATISTICS, una para cada tabla o vista. Todas las instancias de UPDATE STATISTICS usan la misma cláusula, pero con distintos valores de *table_name* o *view_name*. Para más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) y [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md).  
  
> [!IMPORTANT]  
>  El tiempo que tarda la tarea en crear la instrucción Transact-SQL que va a ejecutar es proporcional al número de estadísticas actualizadas por la tarea. Si se configura la tarea para actualizar estadísticas de todas las tablas y vistas de una base de datos que contiene una gran cantidad de índices, o para actualizar las estadísticas de varias bases de datos, la tarea puede tardar mucho tiempo en generar la instrucción Transact-SQL.  
  
## <a name="configuration-of-the-update-statistics-task"></a>Configuración de la tarea Actualizar estadísticas  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Actualizar estadísticas &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
