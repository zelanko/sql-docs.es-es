---
title: Subprocesos (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f39f5ebbb4152046d3d280f2c2f7f90a772348f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109209"
---
# <a name="transact-sql-debugger---threads-window"></a>Depurador de Transact-SQL: ventana Subprocesos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
## <a name="see-also"></a>Ver también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
  
  
