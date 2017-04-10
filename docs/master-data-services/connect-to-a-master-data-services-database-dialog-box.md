---
title: "Conectar a un cuadro de di&#225;logo Base de datos de Master Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.mds.configmanager.srvconnect.f1"
ms.assetid: b2f8c9b9-c31e-4f0d-9095-978709423190
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Conectar a un cuadro de di&#225;logo Base de datos de Master Data Services
  Utilice el cuadro de diálogo **Conectar con una base de datos de Master Data Services** para seleccionar una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 En [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], este cuadro de diálogo se encuentra disponible en las siguientes páginas:  
  
-   En la página **Configuración de base de datos** , haga clic en **Seleccionar base de datos** . Utilice este diálogo para seleccionar una base de datos donde establecer la configuración del sistema.  
  
-   En la página **Configuración web** , en **Asociar aplicación con base de datos**, haga clic en **Seleccionar** para seleccionar la base de datos que se va a asociar con el sitio web o aplicación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## Seleccionar base de datos  
 Especifique la información de conexión a una instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] local o remota que hospede la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para conectarse a una instancia remota, se debe estar habilitado para realizar conexiones remotas.  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Instancia de SQL Server**|Especifique el nombre de la instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que vaya a hospedar a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Puede ser una instancia predeterminada o con nombre en un equipo local o remoto. Especifique la información, para ello escriba:<br /><br /> Un punto (.) para conectarse a la instancia predeterminada en su equipo local.<br /><br /> El nombre del servidor o dirección IP para conectarse a la instancia predeterminada en el equipo local o remoto especificado.<br /><br /> El nombre del servidor o dirección IP y el nombre de instancia para conectarse a la instancia con nombre en el equipo local o remoto especificado. Especifique esta información en el formato *nombre_servidor*\\*nombre_instancia*.|  
|**Tipo de autenticación**|Seleccione el tipo de autenticación que se va a utilizar en la conexión con la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. Las credenciales que use para conectarse determinarán las bases de datos que se van a mostrar en la lista desplegable **Base de datos de Master Data Services**.<br /><br /> Entre los tipos de autenticación se incluyen:<br /><br /> **Usuario actual: Seguridad integrada**: utiliza la autenticación integrada de Windows para la conexión mediante el uso de las credenciales de la cuenta de usuario de Windows actual. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] utiliza las credenciales de Windows del usuario que inició sesión en el equipo y abrió la aplicación. No puede especificar unas credenciales de Windows diferentes en la aplicación. Si desea conectarse con credenciales diferentes de Windows, debe iniciar sesión en el equipo como ese usuario y, a continuación, abrir [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Cuenta de SQL Server**: utiliza una cuenta de SQL Server para la conexión. Al seleccionar esta opción, se habilitan los campos **Nombre de usuario** y **Contraseña** y es preciso que especifique las credenciales para una cuenta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.|  
|**Nombre de usuario**|Especifique el nombre de la cuenta de usuario que se utilizará para conectar a la instancia de SQL Server especificada. La cuenta debe inscribirse en el rol **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada:<br /><br /> Cuando el **Tipo de autenticación** sea **Usuario actual: Seguridad integrada**, el cuadro **Nombre de usuario** es de solo lectura y muestra el nombre de la cuenta de usuario de Windows con la que se ha iniciado sesión en el equipo.<br /><br /> Cuando el **Tipo de autenticación** es **Cuenta de SQL Server**, se habilitará el cuadro **Nombre de usuario** y deberá especificar las credenciales para una cuenta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la instancia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.|  
|**Contraseña**|Especifique la contraseña asociada a la cuenta de usuario:<br /><br /> Cuando el **Tipo de autenticación** sea **Usuario actual: Seguridad integrada**, el cuadro **Contraseña** es de solo lectura y las credenciales de la cuenta de usuario especificada de Windows se usan para conectarse.<br /><br /> Cuando el **Tipo de autenticación** sea **Cuenta de SQL Server**, se habilitará el cuadro **Contraseña** y deberá especificar la contraseña asociada a la cuenta de usuario especificada.|  
|**Connect**|Conéctese a la instancia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con las credenciales especificadas.|  
|**Base de datos de Master Data Services**|Muestra las bases de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada según los siguientes criterios:<br /><br /> Cuando el usuario es un miembro del rol de servidor **sysadmin** para esa instancia, se muestran todas las bases de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en esa instancia.<br /><br /> Cuando el usuario es un miembro del rol de base de datos de **db_owner** para cualquier base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en esa instancia, se muestran esas bases de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].<br /><br/> Para obtener más información sobre los roles de SQL Server, consulte [Roles de nivel de servidor](../relational-databases/security/authentication-access/server-level-roles.md) y [Roles de nivel de base de datos](../relational-databases/security/authentication-access/database-level-roles.md).|  
  
## Vea también  
 [Página Configuración de base de datos &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Introducción a Master Data Services &#40;SQL Server 2016&#41;](../Topic/Get%20Started%20with%20Master%20Data%20Services%20\(SQL%20Server%202016\).md)  
  
  