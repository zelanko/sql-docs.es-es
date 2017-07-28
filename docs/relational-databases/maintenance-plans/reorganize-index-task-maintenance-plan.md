---
title: "Tarea Reorganizar índice (Plan de mantenimiento) | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.defrag.f1
helpviewer_keywords:
- Reorganize Index Task dialog box
ms.assetid: e9cbebbd-f36f-4176-9832-382a46ac946c
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 223d43974e6b63f7375a3d3e000492612fb6856e
ms.openlocfilehash: c07ca6e5a69f368d916c700dbc949726f198af50
ms.contentlocale: es-es
ms.lasthandoff: 07/25/2017

---
# <a name="reorganize-index-task-maintenance-plan"></a>Tarea Reorganizar índice (Plan de mantenimiento)
  Use el cuadro de diálogo **Tarea Reorganizar índice** para mover las páginas del índice en un orden de búsqueda más eficaz. Esta tarea utiliza la instrucción `ALTER INDEX REORGANIZE` con bases de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Conexión**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Bases de datos**  
 Especifique las bases de datos a las que afecta esta tarea.  
  
-   **Todas las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de tempdb.  
  
-   **Todas las bases de datos del sistema**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de **tempdb**. No se ejecutarán tareas de mantenimiento en las bases de datos creadas por usuarios.  
  
-   **Todas las bases de datos de usuario**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos creadas por usuarios. No se ejecutarán tareas de mantenimiento en las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento únicamente en las bases de datos seleccionadas. Si elige esta opción, deberá seleccionar al menos una base de datos de la lista.  
  
 **Objeto**  
 Limite la cuadrícula **Selección** para mostrar tablas, vistas o ambas cosas.  
  
 **Selección**  
 Especifique las tablas o índices que se ven afectados por esta tarea. No estará disponible cuando se seleccione **Tablas y vistas** en el cuadro de diálogo **Objeto** .  
  
 **Compactar objetos grandes**  
 Cancela la asignación de espacio para tablas y vistas cuando es posible. Esta opción utiliza `ALTER INDEX LOB_COMPACTION = ON`.  


[!INCLUDE[index-stats-options-reorg-5589131-2999104](../../includes/paragraph-content/index-stats-options-reorganize-maintenance-plan-include.md)]

  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  

  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **Actualizar**  
 Actualiza la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] with [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Authentication.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication. Esta opción no está disponible.  
  
 **Nombre de usuario.**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Vea también  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [DBCC INDEXDEFRAG &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)  
  
  
