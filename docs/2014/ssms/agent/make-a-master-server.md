---
title: Establecer un servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.msxwiz.complete.f1
- sql12.ag.msxwiz.target.f1
- sql12.ag.msxwiz.login.f1
- sql12.ag.msxwiz.cover.f1
- sql12.ag.msxwiz.operator.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f609af3e4cef804d74772283fc1bb519d3dd89f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163796"
---
# <a name="make-a-master-server"></a>Establecer un servidor maestro
  En este tema se describe cómo establecer un servidor maestro de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para establecer un servidor maestro, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Los trabajos distribuidos que tienen pasos asociados a un proxy se ejecutan bajo el contexto de la cuenta de proxy en el servidor de destino. Para que se descarguen del servidor maestro al de destino los pasos de trabajo asociados con un proxy, asegúrese de que se cumplen las condiciones siguientes:  
  
-   La subclave del registro de servidor maestro **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<*instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName**  (REG_DWORD) se establece en 1 (verdadero). De forma predeterminada, esta subclave está establecida en 0 (false).  
  
-   Existe una cuenta de proxy en el servidor de destino que tiene el mismo nombre que la cuenta de proxy del servidor maestro bajo el que se ejecuta el paso de trabajo.  
  
 Si se producen errores en los pasos de trabajo que utilizan cuentas de proxy durante la descarga de éstos desde el servidor maestro al servidor de destino, puede buscar en la columna **error_message** de la tabla **sysdownloadlist** de la base de datos **msdb** los mensajes de error que digan lo siguiente:  
  
-   "Este trabajo requiere una cuenta de proxy, pero la coincidencia de proxy se ha deshabilitado en el servidor de destino."  
  
     Para resolver este error, establezca la subclave de registro **AllowDownloadedJobsToMatchProxyName** en 1.  
  
-   "No se encontró el proxy".  
  
     Para resolver este error, asegúrese de que existe una cuenta de proxy en el servidor de destino con el mismo nombre que la cuenta de proxy del servidor maestro en la que se ejecuta el paso de trabajo.  
  
####  <a name="Permissions"></a> Permissions  
 Permisos para ejecutar este procedimiento de forma predeterminada a los miembros de la `sysadmin` rol fijo de servidor.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-make-a-master-server"></a>Para establecer un servidor principal  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, a continuación, haga clic en **Hacer que sea principal**. El **Asistente para servidor principal** le guiará en el proceso de establecimiento de un servidor principal y de adición de servidores de destino.  
  
3.  En la página **Operador del servidor maestro** , configure un operador para el servidor maestro. Para enviar notificaciones a los operadores mediante correo electrónico o buscapersonas, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar configurado para enviar correo electrónico. Para enviar notificaciones a los operadores mediante **net send**, el servicio Messenger debe estar en ejecución en el servidor donde reside el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Dirección de correo electrónico**  
     Establece la dirección de correo electrónico del operador.  
  
     **Dirección del buscapersonas**  
     Establece la dirección de correo electrónico de buscapersonas para el operador.  
  
     **Dirección de NET SEND**  
     Establece la dirección de **net send** del operador.  
  
4.  En la página **Servidor de destino** , seleccione servidores de destino para el servidor maestro.  
  
     **Servidores registrados**  
     Muestra los servidores registrados en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] que todavía no son servidores de destino.  
  
     **Servidores de destino**  
     Muestra los servidores que son servidores de destino.  
  
     **>**  
     Mueve el servidor seleccionado a la lista de servidores de destino.  
  
     **>>**  
     Mueve todos los servidores a la lista de servidores de destino.  
  
     **<**  
     Quita el servidor seleccionado de la lista de servidores de destino.  
  
     **<<**  
     Quita todos los servidores de la lista de servidores de destino.  
  
     **Agregar conexión**  
     Agrega un servidor a la lista de servidores de destino sin registrarlo.  
  
     **Conexión**  
     Cambia las propiedades de conexión del servidor seleccionado.  
  
5.  En la página **Credenciales de inicio de sesión del servidor maestro** , especifique si desea crear un nuevo inicio de sesión para el servidor de destino, si es necesario, y asignarle derechos de acceso al servidor maestro.  
  
     **Cree un nuevo inicio de sesión, si es necesario, y asígnele derechos para el servidor maestro**  
     Crea un nuevo inicio de sesión en el servidor de destino si el inicio de sesión especificado ya no existe.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>Para establecer un servidor principal  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se da de alta el servidor actual en el servidor maestro AdventureWorks1. La ubicación del servidor actual es Building 21, Room 309, Rack 5.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
 Para obtener más información, consulte [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Crear un entorno multiservidor](create-a-multiserver-environment.md)   
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)  
  
  
