---
title: Eliminar un proxy del Agente SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79937166e8bbd119f2bb5d5e98b7a49dd969047b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo eliminar una cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para eliminar una cuenta de proxy del Agente SQL Server, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   Cuando elimine una cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , asegúrese de que el proxy no haga referencia a ningún paso de trabajo activo. Para comprobar si existen pasos de trabajo que hacen referencia al proxy, haga clic con el botón derecho en el proxy, seleccione **Propiedades** y, luego, en el cuadro de diálogo *Propiedades de cuenta de proxy***nombre_de_proxy*, seleccione la página **Referencias**. Si elimina un proxy, en el cuadro de diálogo **Eliminar objeto** se le ofrece la posibilidad de volver a asignar todos los pasos de trabajo que utilizan ese proxy.  
  
-   Las cuentas de proxy del Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] utilizan credenciales para almacenar información acerca de las cuentas de usuario de Windows. El usuario especificado en las credenciales debe tener el permiso "Iniciar sesión como proceso por lotes" en el equipo en que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] comprueba el acceso al subsistema de un proxy y da acceso al proxy cada vez que se ejecuta el paso de trabajo. Si el proxy ya no tiene acceso al subsistema, el paso de trabajo da error. De lo contrario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] suplanta al usuario especificado en el proxy y ejecuta el paso de trabajo.  
  
-   Si el inicio de sesión del usuario tiene acceso al proxy o si el usuario pertenece a un rol con acceso al proxy, puede usarlo en un paso de trabajo.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Solo los miembros del rol fijo de servidor **sysadmin** pueden crear, modificar o eliminar cuentas de proxy.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Para eliminar una cuenta de proxy del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la cuenta de proxy que desea eliminar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Servidores proxy** .  
  
4.  Haga clic en el signo más para expandir el subsistema que contiene la cuenta de proxy que desee eliminar (por ejemplo, **Script de ActiveX)**.  
  
5.  Haga clic con el botón derecho en la cuenta de proxy que desea eliminar y seleccione **Eliminar**.  
  
6.  En el cuadro de diálogo **Eliminar objeto** , confirme que esté seleccionada la cuenta de proxy correcta. Active la casilla **Volver a asignar a** para volver a asignar a otra cuenta los pasos de trabajo que hacen referencia a esta cuenta de proxy.  
  
7.  Haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Para eliminar una cuenta de proxy del Agente SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
Para más información, consulte [sp_delete_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c).  
  
