---
title: Pausar o reanudar una sesión de creación de reflejo de la base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resuming database mirroring
- database mirroring [SQL Server], sessions
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: 05ede3b4-6abe-4442-abb7-9f5aee1d6bc0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 361921ec7e0c921c6b534b9d60ef67975e314650
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934117"
---
# <a name="pause-or-resume-a-database-mirroring-session-sql-server"></a>Pausar o reanudar una sesión de creación de reflejo de la base de datos (SQL Server)
  En este tema se describe cómo pausar o reanudar la creación de reflejo de la base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ReplaceThisText con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [después de pausar o reanudar la creación de reflejo de la base de datos](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
 En cualquier momento, puede suspender una sesión de creación de reflejo de la base de datos, lo que puede mejorar el rendimiento durante los cuellos de botella, y puede reanudar una sesión suspendida.  
  
> [!CAUTION]  
>  Después de un servicio forzado, cuando el servidor principal original se vuelve a conectar, se suspende la creación de reflejo. Reanudar la creación de reflejo en esta situación puede dar lugar a una pérdida de datos en el servidor principal original. Para obtener información sobre la administración de la posible pérdida de datos, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Para pausar o reanudar una sesión de creación de reflejo de la base de datos, use la página **Creación de reflejo de Propiedades de la base de datos** .  
  
#### <a name="to-pause-or-resume-database-mirroring"></a>Para pausar o reanudar la creación de reflejo de la base de datos  
  
1.  Durante una sesión de creación de reflejo de la base de datos, conéctese a la instancia de servidor principal y, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Reflejado**. Se abrirá la página **creación de reflejo** del cuadro de diálogo Propiedades de la base de **datos** .  
  
4.  Para pausar la sesión, haga clic en **Pausar**.  
  
     Aparecerá un mensaje de confirmación. Si hace clic en **Sí**, se pausará la sesión y el botón cambiará a **Reanudar**.  
  
     Para obtener más información sobre las repercusiones de pausar una sesión, vea [Pausar y reanudar la creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
5.  Para reanudar la sesión, haga clic en **Reanudar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-pause-database-mirroring"></a>Para pausar la creación de reflejo de la base de datos  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] para cualquier asociado.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Escriba la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente:  
  
     ALTER DATABASE *nombre_de_base_de_datos* SET PARTNER SUSPEND  
  
     donde *nombre_de_base_de_datos* es la base de datos reflejada cuya sesión se quiere suspender.  
  
     En el ejemplo siguiente se pausa la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER SUSPEND;  
    ```  
  
##### <a name="to-resume-database-mirroring"></a>Para reanudar la creación de reflejo de la base de datos  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] para cualquier asociado.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Escriba la instrucción Transact-SQL siguiente:  
  
     ALTER DATABASE *nombre_de_base_de_datos* SET PARTNER RESUME  
  
     donde *nombre_de_base_de_datos* es la base de datos reflejada cuya sesión se quiere reanudar.  
  
     En el ejemplo siguiente se pausa la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER RESUME;  
    ```  
  
##  <a name="follow-up-after-pausing-or-resuming-database-mirroring"></a><a name="FollowUp"></a>Seguimiento: después de pausar o reanudar la creación de reflejo de la base de datos  
  
-   **Después de pausar la creación de reflejo de la base de datos**  
  
     En la base de datos principal, tome precauciones para evitar que se llene el registro de transacciones. Para más información, consulte [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
-   **Después de reanudar la creación de reflejo de la base de datos**  
  
     La reanudación del reflejo de una base de datos pone a la base de datos reflejada en el estado SYNCHRONIZING. Si el nivel de seguridad es FULL, el reflejo se pone al nivel de la principal y la base de datos reflejada toma el estado SYNCHRONIZED. En este punto, es posible una conmutación por error. Si el testigo está presente y activo, es posible la conmutación automática por error. Si no hay un testigo, es posible la conmutación por error manual.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
