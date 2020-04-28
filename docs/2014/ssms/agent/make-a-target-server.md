---
title: Establecer un servidor de destino | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 744ebc5411e626c083676440502489029e888a28
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798187"
---
# <a name="make-a-target-server"></a>Establecer un servidor de destino
  En este tema se describe cómo establecer un servidor de destino en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server (SMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para establecer un servidor de destino, usando**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Los trabajos distribuidos que tienen pasos asociados a un proxy se ejecutan bajo el contexto de la cuenta de proxy en el servidor de destino. Para que se descarguen del servidor maestro al de destino los pasos de trabajo asociados con un proxy, asegúrese de que se cumplen las condiciones siguientes:  
  
-   La subclave del registro del servidor maestro **\\\<HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server*instance_name*> \sql Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) está establecida en 1 (true). De forma predeterminada, esta subclave está establecida en 0 (false).  
  
-   Existe una cuenta de proxy en el servidor de destino que tiene el mismo nombre que la cuenta de proxy del servidor maestro bajo el que se ejecuta el paso de trabajo.  
  
 Si se producen errores en los pasos de trabajo que utilizan cuentas de proxy durante la descarga de éstos desde el servidor maestro al servidor de destino, puede buscar en la columna **error_message** de la tabla **sysdownloadlist** de la base de datos **msdb** los mensajes de error que digan lo siguiente:  
  
-   "Este trabajo requiere una cuenta de proxy, pero la coincidencia de proxy se ha deshabilitado en el servidor de destino."  
  
     Para resolver este error, establezca la subclave de registro **AllowDownloadedJobsToMatchProxyName** en 1.  
  
-   "No se encontró el proxy".  
  
     Para resolver este error, asegúrese de que existe una cuenta de proxy en el servidor de destino con el mismo nombre que la cuenta de proxy del servidor maestro en la que se ejecuta el paso de trabajo.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Los permisos de ejecución de este procedimiento corresponden de forma predeterminada a los miembros del rol fijo de servidor `sysadmin`.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>Para establecer un servidor de destino  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, haga clic en **Establecer como destino**. El **Asistente para establecer servidor de destino** le guiará en el proceso de establecimiento de un servidor de destino.  
  
3.  En la página **Seleccionar un servidor maestro** , seleccione el servidor maestro del que este servidor de destino recibirá trabajos.  
  
     **Seleccionar servidor**  
     Conéctese al servidor principal.  
  
     **Descripción de este servidor**  
     Escriba una descripción para este servidor de destino. El servidor de destino carga esta descripción en el servidor principal.  
  
4.  En la página **Credenciales de inicio de sesión del servidor maestro** , cree un nuevo inicio de sesión en el servidor de destino, si es necesario.  
  
     **Cree un nuevo inicio de sesión, si es necesario, y asígnele derechos para el servidor maestro**  
     Crea un nuevo inicio de sesión en el servidor de destino si el inicio de sesión especificado ya no existe.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>Para establecer un servidor de destino  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se da de alta el servidor actual en el servidor maestro AdventureWorks1. La ubicación del servidor actual es Building 21, Room 309, Rack 5.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     Para obtener más información, vea [sp_msx_enlist &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>Usar Objetos de administración de SQL Server (SMO)  
  
## <a name="see-also"></a>Consulte también  
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)  
