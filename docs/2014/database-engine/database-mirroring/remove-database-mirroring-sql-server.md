---
title: Quitar la creación de reflejo de la base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aae710069fbb8c27a8e94e3c26d35f04c935246d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297055"
---
# <a name="remove-database-mirroring-sql-server"></a>Quitar la creación de reflejo de la base de datos (SQL Server)
  En este tema se describe cómo quitar la creación de reflejo de una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  El propietario de la base de datos puede detener manualmente en cualquier momento una sesión de creación de reflejo de la base de datos quitando el reflejo de la base de datos.  
  
 
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>Para quitar la creación de reflejo de la base de datos  
  
1.  Durante una sesión de creación de reflejo de la base de datos, conéctese a la instancia de servidor principal y, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Reflejado**. Así se abre la página **Creación de reflejo** del cuadro de diálogo **Propiedades de la base de datos** .  
  
4.  En el panel **Seleccionar una página** , haga clic en **Creación de reflejos**.  
  
5.  Para quitar la creación de reflejo, haga clic en **Quitar creación de reflejo**. Aparecerá un mensaje de confirmación. Si hace clic en **Sí**, se detendrá la sesión y la creación de reflejo se quitará de la base de datos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para quitar la creación de reflejo de la base de datos, use las **Propiedades de la base de datos**. Use la página **Creación de reflejo** del cuadro de diálogo **Propiedades de la base de datos** .  
  
#### <a name="to-remove-database-mirroring"></a>Para quitar la creación de reflejo de la base de datos  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] de algún asociado de creación de reflejo.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Escriba la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente:  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     Donde *database_name* es la base de datos reflejada cuya sesión quiere quitar.  
  
     En el ejemplo siguiente se quita la creación de reflejo de la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="FollowUp"></a> Seguimiento: quitar la creación de reflejo de la base de datos  
  
> [!NOTE]  
>  Para obtener más información sobre las repercusiones de quitar la creación de reflejo, vea [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
-   **Si piensa reiniciar la creación de reflejo de la base de datos**  
  
     Debe aplicar a la base de datos reflejada las copias de seguridad de registros realizadas en la base de datos principal después de quitar la creación de reflejo antes de poder reiniciar la creación de reflejo.  
  
-   **Si no piensa reiniciar la creación de reflejo**  
  
     Opcionalmente, puede recuperar la base de datos reflejada anterior. En la instancia de servidor que era el servidor reflejado, puede usar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente:  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  Si recupera esta base de datos, habrá dos bases de datos divergentes en línea con el mismo nombre. Por consiguiente, debe garantizar que los clientes tengan acceso solamente a una de ellas, generalmente la base de datos principal más reciente.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Pausar o reanudar una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [Quitar el testigo de una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [Ejemplo: configurar la creación de reflejo de la base de datos con certificados &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Configurar la creación de reflejo de la base de datos &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn (SQL Server)](../availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
