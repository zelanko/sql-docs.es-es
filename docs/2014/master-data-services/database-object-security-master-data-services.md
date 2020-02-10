---
title: Seguridad de objetos de base de datos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], object security
- security [Master Data Services], database objects
ms.assetid: dd5ba503-7607-45d9-ad0d-909faaade179
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3eafc9720197ffc32cdca2ef58f91725befaaec1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483154"
---
# <a name="database-object-security-master-data-services"></a>Seguridad de objetos de base de datos (Master Data Services)
  En la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , los datos están almacenados en varias tablas de base de datos y se ven en las vistas. La información que pueda haber protegido en la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] está visible para los usuarios con acceso a la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 En concreto, la información del sueldo de los empleados podría estar contenida en un modelo Empleado, o la información financiera de la compañía podría estar en un modelo Cuenta. Puede denegar el acceso a un usuario a estos modelos en la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , pero los usuarios con acceso a la base de datos pueden ver estos datos.  
  
 Puede conceder permisos a los objetos de base de datos para hacer que datos concretos estén disponibles para los usuarios. Para obtener más información sobre cómo conceder permisos, consulte [GRANT &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql). Para obtener más información acerca de cómo proteger un servidor SQL Server, vea [Securing SQL Server](../relational-databases/security/securing-sql-server.md).  
  
 Las siguientes tareas necesitan acceso a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] :  
  
-   [Datos de almacenamiento provisional](#Staging)  
  
-   [Validar datos según las reglas de negocios](#rules)  
  
-   [Eliminar versiones](#Versions)  
  
-   [Aplicar inmediatamente los permisos de los miembros de la jerarquía](#Hierarchy)  
  
-   [Cambio de la cuenta del administrador del sistema](#SysAdmin)  
  
-   [Configuración del sistema](#SysSettings)  
  
##  <a name="Staging"></a>Datos de almacenamiento provisional  
 En la tabla siguiente, cada elemento protegible tiene "name" como parte del nombre. Indica el nombre de la tabla de ensayo que se especificó cuando se creó una entidad. Para obtener más información, vea [&#40;de importación de datos Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
|Acción|Elementos protegibles|Permisos|  
|------------|----------------|-----------------|  
|Cargar miembros hoja y sus atributos en la tabla de ensayo.|stg.name_Leaf|Obligatorio: INSERT<br /><br /> Opcional: SELECT y UPDATE|  
|Cargar datos de la tabla de ensayo Leaf en las tablas adecuadas de la base de datos de MDS.|stg.udp_name_Leaf|Ejecute|  
|Cargar miembros consolidados y sus atributos en la tabla de ensayo.|stg.name_Consolidated|Obligatorio: INSERT<br /><br /> Opcional: SELECT y UPDATE|  
|Cargar los datos de la tabla de ensayo Consolidated en las tablas adecuadas de la base de datos de MDS.|stg.udp_name_Consolidated|Ejecute|  
|Cargue relaciones de miembros hoja y consolidados entre sí en una jerarquía explícita en la tabla de ensayo.|stg.name_Relationship|Obligatorio: INSERT<br /><br /> Opcional: SELECT y UPDATE|  
|Cargar los datos de la tabla de ensayo Relationship en las tablas adecuadas de la base de datos de MDS.|stg.udp_name_Relationship|Ejecute|  
|Ver los errores producidos cuando se insertaban datos de las tablas de ensayo en tablas de la base de datos de MDS.|stg.udp_name_Relationship|SELECT|  
  
 Para más información, vea [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
##  <a name="rules"></a>Validar datos según las reglas de negocios  
  
|Acción|Elemento protegible|Permisos|  
|------------|---------------|-----------------|  
|Validar una versión de datos según las reglas de negocios|mdm.udpValidateModel|Ejecute|  
  
 Para obtener más información, consulte [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md).  
  
##  <a name="Versions"></a>Eliminar versiones  
  
|Acción|Elementos protegibles|Permisos|  
|------------|----------------|-----------------|  
|Determinar el identificador de la versión que desea eliminar|mdm.viw_SYSTEM_SCHEMA_VERSION|SELECT|  
|Eliminar una versión de un modelo|mdm.udpVersionDelete|Ejecute|  
  
 Para obtener más información, consulte [Eliminar una versión &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-version-master-data-services.md).  
  
##  <a name="Hierarchy"></a>Aplicar inmediatamente los permisos de los miembros de la jerarquía  
  
|Acción|Elementos protegibles|Permisos|  
|------------|----------------|-----------------|  
|Aplicar los permisos de los miembros inmediatamente|mdm.udpSecurityMemberProcessRebuildModel|Ejecute|  
  
 Para más información, vea [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
##  <a name="SysAdmin"></a>Cambio de la cuenta de administrador del sistema  
  
|Acción|Elementos protegibles|Permisos|  
|------------|----------------|-----------------|  
|Determinar el SID del nuevo administrador|mdm.tblUser|SELECT|  
|Cambiar la cuenta del administrador del sistema|mdm.udpSecuritySetAdministrator|Ejecute|  
  
 Para obtener más información, vea [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
##  <a name="SysSettings"></a>Configuración del sistema  
 Hay opciones del sistema que puede configurar para controlar el comportamiento en [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Puede ajustar estos valores en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o, si tiene el acceso ACTUALIZAR, puede ajustarlos directamente en la tabla de base de datos mdm.tblSystemSetting. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte también  
 [Master Data Services de &#40;de seguridad&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
