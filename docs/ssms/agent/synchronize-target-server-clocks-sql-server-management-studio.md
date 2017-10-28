---
title: Sincronizar los relojes de los servidores de destino (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cacbf8f58717dca6613810ab0b90edcca0df4c83
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Sincronizar los relojes de los servidores de destino (SQL Server Management Studio)
En este tema se describe cómo sincronizar los relojes de los servidores de destino en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] con el reloj del servidor maestro mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)]. La sincronización de los relojes del sistema admite la programación de trabajos.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para sincronizar los relojes de los servidores de destino, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar los relojes de los servidores de destino  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor donde desea sincroniza los relojes de los servidores de destino con el reloj del servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración multiservidor**y seleccione **Administrar servidores de destino**.  
  
3.  En el cuadro de diálogo **Administrar servidores de destino** , haga clic en **Exponer instrucciones**.  
  
4.  En la lista **Tipo de instrucción** , seleccione **Sincronizar relojes**.  
  
5.  En **Destinatarios**, realice una de las siguientes acciones:  
  
    -   Haga clic en **Todos los servidores de destino** para sincronizar los relojes de todos los servidores de destino con el reloj del servidor maestro.  
  
    -   Haga clic en **Estos servidores de destino** para sincronizar determinados relojes de servidores y, a continuación, seleccione cada servidor de destino cuyo reloj desee sincronizar con el reloj del servidor maestro.  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar los relojes de los servidores de destino  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
Para más información, consulte [sp_resync_targetserver (Transact-SQL)](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f).  
  

