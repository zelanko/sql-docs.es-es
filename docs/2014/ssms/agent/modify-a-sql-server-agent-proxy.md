---
title: Modificar un proxy del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], modifying
- modifying SQL Server Agent proxy
ms.assetid: 6e1dfbaa-8089-4813-940c-d5a2e13d8552
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d557afd541ebd3d04702ced7e4275aca2845bf17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226598"
---
# <a name="modify-a-sql-server-agent-proxy"></a>Modificar un proxy del Agente SQL Server
  En este tema se describe cómo modificar un proxy del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para modificar un proxy del Agente SQL Server, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las cuentas de proxy del Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan credenciales para almacenar información acerca de las cuentas de usuario de Windows. El usuario especificado en las credenciales debe tener el permiso "Iniciar sesión como proceso por lotes" en el equipo en que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comprueba el acceso al subsistema de un proxy y da acceso al proxy cada vez que se ejecuta el paso de trabajo. Si el proxy ya no tiene acceso al subsistema, el paso de trabajo da error. De lo contrario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suplanta al usuario especificado en el proxy y ejecuta el paso de trabajo.  
  
-   Si el inicio de sesión del usuario tiene acceso al proxy o si el usuario pertenece a un rol con acceso al proxy, puede usarlo en un paso de trabajo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden crear, modificar o eliminar cuentas de proxy.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversion-mdmd-agent-proxy"></a>Para modificar un proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea modificar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Servidores proxy** .  
  
4.  Haga clic en el signo más para expandir el nodo del subsistema para el proxy (por ejemplo, **Script ActiveX**).  
  
5.  Haga clic con el botón derecho en la cuenta de proxy que desee modificar y seleccione **Propiedades**.  
  
6.  En el cuadro de diálogo *Propiedades de cuenta de proxy***nombre_de_proxy*, realice los cambios que considere necesarios en la cuenta de proxy. Para más información acerca de las opciones de este cuadro de diálogo, consulte [Crear un proxy del Agente SQL Server](create-a-sql-server-agent-proxy.md).  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversion-mdmd-agent-proxy"></a>Para modificar un proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Disables the proxy named 'Catalog application proxy'.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 0;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_update_proxy &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-proxy-transact-sql).  
  
  
