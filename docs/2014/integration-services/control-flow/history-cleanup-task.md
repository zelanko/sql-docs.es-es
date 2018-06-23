---
title: Tarea Limpieza de historial | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3f25531b3dd2df5fa43bc0dcaa3ea0decc9d7386
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198490"
---
# <a name="history-cleanup-task"></a>Tarea Limpieza de historial
  La tarea Limpieza de historial elimina entradas de las siguientes tablas de historial de la base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 Un paquete puede utilizar la tarea Limpieza del historial para eliminar datos históricos relacionados con las actividades de copias de seguridad y restauración, trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y planes de mantenimiento de bases de datos.  
  
 Esta tarea encapsula el procedimiento almacenado del sistema sp_delete_backuphistory y pasa la fecha especificada al procedimiento como un argumento. Para más información, vea [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql).  
  
## <a name="configuration-of-the-history-cleanup-task"></a>Configuración de la tarea Limpieza de historial  
 La tarea incluye una propiedad para especificar la fecha más antigua de los datos almacenados en las tablas de historial. Puede indicar la fecha mediante el número de días, semanas, meses o años del día actual, y la tarea traducirá automáticamente el intervalo a una fecha.  
  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Limpieza de historial &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
