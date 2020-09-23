---
description: Sincronización de los relojes de los servidores de destino
title: Sincronización de los relojes de los servidores de destino
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9c0804658359c1272bfe4acb025fbded3ae2adc7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463027"
---
# <a name="synchronize-target-server-clocks"></a>Sincronización de los relojes de los servidores de destino

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

En este tema se describe cómo sincronizar los relojes de los servidores de destino en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el reloj del servidor maestro mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La sincronización de los relojes del sistema admite la programación de trabajos.  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar los relojes de los servidores de destino  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor donde desea sincroniza los relojes de los servidores de destino con el reloj del servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración multiservidor**y seleccione **Administrar servidores de destino**.  
  
3.  En el cuadro de diálogo **Administrar servidores de destino** , haga clic en **Exponer instrucciones**.  
  
4.  En la lista **Tipo de instrucción** , seleccione **Sincronizar relojes**.  
  
5.  En **Destinatarios**, realice una de las siguientes acciones:  
  
    -   Haga clic en **Todos los servidores de destino** para sincronizar los relojes de todos los servidores de destino con el reloj del servidor maestro.  
  
    -   Haga clic en **Estos servidores de destino** para sincronizar determinados relojes de servidores y, a continuación, seleccione cada servidor de destino cuyo reloj desee sincronizar con el reloj del servidor maestro.  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usar Transact-SQL  
  
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
  
Para más información, consulte [sp_resync_targetserver (Transact-SQL)](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f).  
  
