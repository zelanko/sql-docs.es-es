---
title: Servidores remotos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6221a1b271386b685d7b99baf5ebecc0a5e0b506
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="remote-servers"></a>Servidores remotos
  Los servidores remotos solo se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por compatibilidad con versiones anteriores. No obstante, las aplicaciones nuevas deben utilizar servidores vinculados. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).  
  
 Una configuración de servidor remoto permite a un cliente conectado a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutar un procedimiento almacenado en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin necesidad de establecer una conexión individual. En cambio, el servidor al que está conectado el cliente acepta la solicitud de cliente y la envía al servidor remoto en nombre del cliente. El servidor remoto procesa la solicitud y devuelve todos los resultados al servidor original. Este servidor, a su vez, pasa esos resultados al cliente. Cuando configura un servidor remoto, también debe tener en cuenta los aspectos de seguridad.  
  
 Si desea configurar un servidor para ejecutar procedimientos almacenados en otro servidor y no dispone de configuraciones de servidores remotos existentes, use servidores vinculados en lugar de servidores remotos. Se permiten procedimientos almacenados y consultas distribuidas en servidores vinculados; sin embargo, solo se permiten procedimientos almacenados en servidores remotos.  
  
## <a name="remote-server-details"></a>Detalles de servidores remotos  
 Los servidores remotos se configuran en pares. Para configurar un par de servidores remotos, configure ambos servidores para reconocerse mutuamente como servidores remotos.  
  
 La mayoría de las veces, no debe establecer opciones de configuración para los servidores remotos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establece valores predeterminados en los equipos local y remoto a fin de permitir conexiones de servidores remotos.  
  
 Para que el acceso al servidor remoto funcione correctamente, la opción de configuración **remote access** se debe establecer en 1 tanto en el equipo local como en el remoto. (Esta es la configuración predeterminada).  **remote access** controla los inicios de sesión desde servidores remotos. Es posible restablecer esta opción de configuración con el procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para establecer la opción en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en la página **Conexiones de Propiedades del servidor** , use **Permitir conexiones remotas con este servidor**. Para llegar a la página **Conexiones de Propiedades del servidor** , en el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, luego, haga clic en **Propiedades**. En la página **Propiedades del servidor** , haga clic en la página **Conexiones** .  
  
 Desde el servidor local, puede deshabilitar una configuración de servidor remoto para impedir el acceso a ese servidor local por parte de usuarios que se encuentran en el servidor remoto con el que se complementa.  
  
## <a name="security-for-remote-servers"></a>Seguridad para servidores remotos  
 Para habilitar las llamadas a procedimiento remoto (RPC) en servidores remotos, es preciso configurar asignaciones de inicios de sesión en el servidor remoto (y tal vez en el servidor local) en que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las llamadas a procedimiento remoto están deshabilitadas de forma predeterminada. Esta configuración mejora la seguridad del servidor al reducir el área expuesta susceptible de ser atacada. Debe habilitar esta característica para poder usar RPC. Para obtener más información, vea [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
### <a name="setting-up-the-remote-server"></a>Configurar el servidor remoto  
 Es necesario configurar asignaciones de inicios de sesión remotos en el servidor remoto. Con estas asignaciones, el servidor remoto asigna el inicio de sesión entrante para una conexión de RPC desde el servidor especificado hasta un inicio de sesión local. Para configurar asignaciones de inicios de sesión remotos, use el procedimiento almacenado **sp_addremotelogin** en el servidor remoto.  
  
> [!NOTE]  
>  La opción **trusted** de  **sp_remoteoption** no se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="setting-up-the-local-server"></a>Configurar el servidor local  
 Para inicios de sesión local autenticados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no es necesario establecer una asignación de inicio de sesión en el servidor local. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el inicio de sesión local y password para conectarse al servidor remoto. Para los inicios de sesión autenticados de Windows, configure una asignación de inicio de sesión local en un servidor local que defina el inicio de sesión y la contraseña que utilizará una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al establecer una conexión de RPC a un servidor remoto.  
  
 Para los inicios de sesión creados por la autenticación de Windows, debe crear una asignación a un nombre de inicio de sesión y una contraseña a través del procedimiento almacenado **sp_addlinkedservlogin** . Este nombre de inicio de sesión y esta contraseña deben coincidir con el inicio de sesión entrante y la contraseña que espera el servidor remoto, creados por medio de **sp_addremotelogin**.  
  
> [!NOTE]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
### <a name="remote-server-security-example"></a>Ejemplo de seguridad para servidores remotos  
 Considere las instalaciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siguientes: **serverSend** and **serverReceive**. **serverReceive** está configurado para asignar un inicio de sesión entrante de **serverSend**, denominado **Sales_Mary**, a un inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticado de **serverReceive**, llamado **Alice**. Otro inicio de sesión entrante de **serverSend**, llamado **Joe**, está asignado a un inicio de sesión autenticado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en **serverReceive***,* llamado **Joe**.  
  
 En el siguiente ejemplo de código de Transact-SQL se configura `serverSend` para realizar llamadas RPC en `serverReceive`.  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 En `serverSend`, se crea una asignación de inicio de sesión local para el inicio de sesión autenticado de Windows `Sales\Mary` al inicio de sesión `Sales_Mary`. No se necesita ninguna asignación local para `Joe`, ya que la opción predeterminada es usar el mismo nombre de inicio de sesión y contraseña, y `serverReceive` contiene una asignación para `Joe`.  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>Ver propiedades de servidores locales o remotos  
 Use el procedimiento almacenado extendido **xp_msver** para revisar los atributos de servidor de servidores locales o remotos. Estos atributos incluyen el número de versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el tipo y número de procesadores del equipo y la versión del sistema operativo. Desde el servidor local, puede ver bases de datos, archivos, inicios de sesión y herramientas de servidores remotos. Para obtener más información, vea [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [Configurar la opción de configuración del servidor Acceso remoto](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
