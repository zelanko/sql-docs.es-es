---
title: Roles y tareas de Reporting Services frente a grupos y permisos de SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e9b7a33cebdfb6772460087a4cd9841f6b859ac1
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305903"
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Roles y tareas de Reporting Services frente a grupos y permisos de SharePoint
  En este tema se comparan las características de autorización basadas en roles y tareas en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con las características de seguridad de los productos de SharePoint. En este tema se comparan la terminología y las características de los roles, las tareas, los grupos de SharePoint, los niveles de permiso y los permisos.  
  
||  
|-|  
| [!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint &#124; SharePoint 2010 y SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo|  
  
 **En este tema:**  
  
-   [Comparación de las herramientas y la terminología de permisos](#bkmk_compare_tools_terms)  
  
-   [Comparación de los roles de modo nativo y los grupos de SharePoint](#bkmk_compare_roles_groups)  
  
-   [Comparación de las tareas de modo nativo y los permisos de SharePoint](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> Comparación de las herramientas y la terminología de permisos  
 **Modo nativo:** los objetos de permiso en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (roles y tareas) se crean en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y se configuran para los usuarios individuales en el Administrador de informes.  
  
 **Modo de SharePoint:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa las características de permisos de SharePoint. Los grupos y los permisos de SharePoint se administran desde la página **Configuración del sitio** .  
  
 En la tabla siguiente se comparan los objetos y conceptos relacionados con los permisos entre el modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y SharePoint.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo|SharePoint|  
|---------------------------------------------|----------------|  
|**Rol:** por ejemplo, "Administrador de contenido".|**Grupo:** por ejemplo, el grupo predeterminado "Visores".|  
|---|**Grupo de nivel de permisos:** por ejemplo, "Solo ver" para el grupo "Visores".|  
|**Tareas:** por ejemplo, "Administrar informes".|**Permisos:** por ejemplo, dentro del grupo "Solo ver" hay permisos relacionados con listas para ver elementos, ver versiones y ver páginas de aplicación.|  
  
 Para obtener más información sobre los permisos de SharePoint, vea [Niveles de permisos y permisos](https://support.office.com/en-us/article/Understand-groups-and-permissions-on-a-SharePoint-site-258E5F33-1B5A-4766-A503-D86655CF950D) y [Determinar grupos y niveles de permisos en SharePoint 2013](https://technet.microsoft.com/library/cc262690.aspx).  
  
##  <a name="bkmk_compare_roles_groups"></a> Comparación de los roles de modo nativo y los grupos de SharePoint  
 En la tabla siguiente se comparan las definiciones de roles predefinidas en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo con las de los grupos de SharePoint estándar. Si los grupos de SharePoint no coinciden con el rol específico que desea, puede crear un grupo personalizado y asignar niveles de permiso en SharePoint.  
  
 **Nota**: Los grupos predeterminados de SharePoint disponibles dependen de la plantilla de sitio usada para crear el sitio de SharePoint.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Rol|Grupos de SharePoint|  
|--------------------------------------|-----------------------|  
|**Browser**<br /><br /> Ver|Use el grupo **Visitantes** para conceder permisos para ver informes. El grupo **Visitantes** tiene permisos del nivel de lectura, lo que permite a los miembros del grupo ver páginas, elementos de lista y documentos.|  
|**Administrador de contenido**<br /><br /> Permisos totales para todos los elementos y operaciones de nivel de elemento, incluidos los permisos para establecer la seguridad.|Use el grupo **Propietarios** para conceder un control total sobre la administración de los elementos del servidor de informes en un sitio de SharePoint. El grupo **Propietarios** tiene permisos de control total, lo que permite a los miembros del grupo realizar cambios en el contenido, las páginas o la funcionalidad del sitio. El acceso de control total debe estar limitado solamente a los administradores del sitio.|  
|**Mis informes**|No hay ningún grupo equivalente. **Mis informes** no se admite para un servidor de informes que se ejecuta en modo de SharePoint. Puede usar las características de Mis informes en [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] si desea usar la funcionalidad equivalente.|  
|**publicador**<br /><br /> Agregar, actualizar, ver y eliminar informes, modelos de informe, orígenes de datos compartidos y recursos.|Use el grupo **Miembros** para conceder permisos para agregar elementos, editar elementos y actualizar referencias a elementos dependientes en un sitio de SharePoint. El grupo **Miembros** tiene permisos del nivel Colaborar, lo que permite a los miembros del grupo ver páginas, agregar y actualizar elementos, así como enviar cambios para su aprobación.|  
|**Generador de informes**<br /><br /> Ver informes, administrar automáticamente la suscripción individual y abrir informes en el Generador de informes.|No hay ningún nivel de permiso o grupo de SharePoint predefinido que sea equivalente a la definición de informe del Generador de informes. De manera predeterminada, los usuarios que pertenecen al grupo **Miembros** o **Propietarios** tienen permiso para usar el Generador de informes. Si desea que el Generador de informes esté disponible para más usuarios, debe crear una configuración de seguridad personalizada para proporcionar un nivel de permiso similar al que ofrece el rol Generador de informes. Para obtener más información, vea [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md).|  
|-|Use el grupo de **Visores** para conceder permisos para ver los informes representados. El grupo **Visores** no puede descargar ni ver el contenido de los elementos de informe.<br /><br /> **Nota:** A partir de SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el grupo **Visores** no tiene permisos para crear suscripciones.|  
|**Usuario del sistema** y **Administrador del sistema**|Estos roles no son necesarios para un servidor de informes que se ejecuta en modo de SharePoint. **Usuario del sistema** y **Administrador del sistema** se corresponden con los permisos del nivel de conjunto de servidores o aplicación web de SharePoint. El servidor de informes no proporciona ninguna funcionalidad que requiera una autorización en dicho nivel.|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> Comparación de las tareas de modo nativo y los permisos de SharePoint  
 En la tabla siguiente se comparan las tareas de modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con los permisos de SharePoint. La columna **Tipo** indica si la tarea en modo nativo está relacionada con un rol del sistema o con roles y elementos estándar. Los roles del sistema administran los permisos en el nivel del sistema, como programaciones compartidas.  
  
|Tarea de modo nativo|Tipo de rol|Permiso de SharePoint equivalente|  
|----------------------|---------------|--------------------------------------|  
|Usar informes|Elemento|Editar elementos, Ver elementos.|  
|Crear informes vinculados|Elemento|No compatible.|  
|Administrar todas las suscripciones|Elemento|Administrar alertas.|  
|Administrar orígenes de datos|Elemento|Agregar elementos, Editar elementos, Eliminar elementos, Ver elementos.|  
|Administrar carpetas|Elemento|Agregar elementos, Editar elementos, Eliminar elementos, Ver elementos.|  
|Administrar suscripciones individuales|Elemento|Editar elementos<br /><br /> Antes de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el nivel de permiso necesario era Crear alertas.|  
|Administrar modelos|Elemento|Agregar elementos, Editar elementos, Eliminar elementos, Ver elementos.|  
|Administrar historial de informe|Elemento|Editar elementos, Ver versiones, Eliminar versiones.|  
|Administrar informes|Elemento|Agregar elementos, Editar elementos, Eliminar elementos, Ver elementos.|  
|Administrar recursos|Elemento|Agregar elementos, Editar elementos, Eliminar elementos, Ver elementos.|  
|Establecer la seguridad de elementos individuales|Elemento|Administrar permisos|  
|Ver orígenes de datos|Elemento|Ver elementos.|  
|Ver carpetas|Elemento|Ver elementos.|  
|Ver modelos|Elemento|Ver elementos.|  
|Ver informes|Elemento|Ver elementos.|  
|Ver recursos|Elemento|Ver elementos.|  
||||  
|Ejecutar definiciones de informe|Sistema|Ver elementos.|  
|Generar eventos|Sistema|Administración del sitio web.|  
|Administrar trabajos|Sistema|Ninguno (no compatible).|  
|Administrar propiedades del servidor de informes|Sistema|Ninguno (no aplicable). El servidor de informes no controla si el usuario tiene permiso para ver la configuración de la integración en la Administración central.|  
|Administrar roles|Sistema|Administrar permisos.|  
|Administrar programaciones compartidas|Sistema|Administración del sitio Web, Abrir.|  
|Administrar la seguridad del servidor de informes|Sistema|Ninguno (no aplicable). El servidor de informes no usa asignaciones de roles de nivel de sistema en un servidor que se ejecuta en el modo integrado de SharePoint.|  
|Ver propiedades del servidor de informes|Sistema|Ninguno (no aplicable). El servidor de informes no controla si el usuario tiene permiso para ver la configuración de la integración en la Administración central.|  
|Ver programaciones compartidas|Sistema|Abrir elementos.|  
  
## <a name="see-also"></a>Consulte también  
 [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Establecimiento de permisos para las operaciones del servidor de informes en una aplicación web de SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Definiciones de roles](../../reporting-services/security/role-definitions.md)   
 [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
