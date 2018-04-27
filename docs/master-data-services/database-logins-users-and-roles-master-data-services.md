---
title: Inicios de sesión, usuarios y roles en bases de datos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d3e96e8535289acd3da265595cc58624bea1c0f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="database-logins-users-and-roles-master-data-services"></a>Inicios de sesión, usuarios y roles en bases de datos (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] incluye inicios de sesión, usuarios y roles que se instalan automáticamente en la instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que hospeda la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . No se deberían modificar estos inicios de sesión, usuarios y roles.  
  
## <a name="logins"></a>Inicios de sesión  
  
|Login|Description|  
|-----------|-----------------|  
|**mds_dlp_login**|Permite la creación de ensamblados de UNSAFE. Para más información, consulte [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).<br /><br /> -Inicio de sesión deshabilitado con contraseña generada de forma aleatoria.<br /><br /> -Asigna dbo para la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> -Para msdb, mds_clr_user asigna este inicio de sesión.|  
|**mds_email_login**|Inicio de sesión habilitado usado para las notificaciones.<br /><br /> Para msdb y la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , mds_email_user asigna este inicio de sesión.|  
  
## <a name="msdb-users"></a>Usuarios de msdb  
  
|Usuario|Description|  
|----------|-----------------|  
|**mds_clr_user**|No se usa. Asigna mds_dlp_login.|  
|**mds_email_user**|Se usa para notificaciones.<br /><br /> -Asigna mds_email_login.<br /><br /> -Es un miembro del rol: DatabaseMailUserRole.|  
  
## <a name="master-data-services-database-users"></a>Usuarios de la base de datos de Master Data Services  
  
|Usuario|Description|  
|----------|-----------------|  
|**mds_email_user**|Se usa para notificaciones.<br /><br /> -Tiene el permiso SELECT para el esquema de mdm.<br /><br /> -Tiene el permiso EXECUTE para el tipo de tabla definida por el usuario mdm.MemberGetCriteria.<br /><br /> -Tiene el permiso EXECUTE para el procedimiento almacenado mdm.udpNotificationQueueActivate.|  
|**mds_schema_user**|Posee los esquemas de mdq y mdm. El esquema predeterminado es mdm.<br /><br /> No tiene un inicio de sesión asignado a él.|  
|**mds_ssb_user**|Se usa para ejecutar tareas de Service Broker.<br /><br /> -Tiene todos los esquemas de permisos para DELETE, INSERT, REFERENCES, SELECT y UPDATE.<br /><br /> -No tiene un inicio de sesión asignado a él.|  
  
## <a name="master-data-services-database-role"></a>Rol de la base de datos Master Data Services  
  
|Rol|Description|Permisos|  
|----------|-----------------|-----------------|  
|**mds_exec**|Este rol contiene la cuenta que se ha designado en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] al crear una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] y designa una cuenta para el grupo de aplicaciones.|Permiso EXECUTE en todos los esquemas.<br /><br /> <br /><br /> Permiso ALTERT, INSERT y SELECT en estas tablas:<br /><br /> mdm.tblStgMember<br /><br /> mdm.tblStgMemberAttribute<br /><br /> mdm.tbleStgRelationship<br /><br /> <br /><br /> Permiso SELECT en estas tablas:<br /><br /> mdm.tblUser<br /><br /> mdm.tblUserGroup<br /><br /> mdm.tblUserPreference<br /><br /> <br /><br /> Permiso SELECT en estas vistas:<br /><br /> mdm.viw_SYSTEM_SECURITY_NAVIGATION<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br /><br /> mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>Esquemas  
  
|Rol|Description|  
|----------|-----------------|  
|**mdm**|Contiene todos los objetos de Service Broker y bases de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que no sean las funciones contenidas en el esquema mdq.|  
|**mdq**|Contiene funciones de base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] relacionadas con el filtrado de los resultados de miembros basados en expresiones regulares o de similitud, y el formato de los correos electrónicos de notificación.|  
|**stg**|Contiene las tablas de bases de datos, los procedimientos almacenados y las vistas de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] relacionadas con el proceso de almacenamiento provisional. No elimine ninguno de estos objetos. Para obtener más información sobre el proceso de almacenamiento provisional, consulte [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).|  
  
## <a name="see-also"></a>Ver también  
 [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)  
  
  
