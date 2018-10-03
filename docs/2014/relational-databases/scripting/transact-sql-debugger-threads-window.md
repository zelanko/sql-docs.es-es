---
title: Subprocesos (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5de9e718d68accf108a24474926c0c67c1d4ef2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092155"
---
# <a name="threads-window"></a>Ventana de subprocesos
  La ventana **Subprocesos** muestra información sobre el subproceso de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que usa la sesión del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se está depurando. Debe estar en modo de depuración para mostrar la información del subproceso.  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a la ventana Subprocesos**  
  
-   En el menú **Depurar** , haga clic en **Ventanas**y, a continuación, haga clic en **Subprocesos**.  
  
## <a name="columns"></a>Columnas  
 **ID**  
 Es un número de identificación único que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] asigna al subproceso. Puede encontrar más información sobre el subproceso seleccionando una fila de la vista de administración dinámica sys.dm_os_threads.  
  
 Si no está usando el modo de agrupación ligera, seleccione la fila en la que el valor de os_thread_id coincide con el valor de la columna **ID** . Si está usando el modo de agrupación ligera, seleccione la fila en la que el valor en fiber_context_address coincide con el valor de la columna **ID** .  
  
 **Nombre**  
 Muestra información sobre la sesión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el formato **nombreDeEquipo/nombreDeInstancia [SPID]**.  
  
 **nombreDeEquipo**  
 Nombre del equipo que ejecuta la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] a la que la sesión del Editor de consultas está conectada.  
  
 **InstanceName**  
 Nombre de la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] a la que la sesión del Editor de consultas está conectada.  
  
 **[SPID]**  
 Identificador del proceso de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que identifica de forma única esta sesión. Puede obtener más información sobre la sesión seleccionando la fila en la vista sys.sysprocesses que tenga el mismo valor en la columna spid.  
  
 **Ubicación**  
 Muestra el nombre del archivo de script que se utiliza en la sesión del Editor de consultas que se está depurando.  
  
 **Prioridad**  
 El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] no admite esta característica.  
  
 **Suspender**  
 El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] no admite esta característica.  
  
## <a name="see-also"></a>Vea también  
 [Depurador de Transact-SQL](transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql)  
  
  
