---
title: Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 40622ae8099450acce3274937a46adc43c37fdb0
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43267881"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ofrece características de seguridad integradas que puede usar para conceder acceso a los elementos del servidor de informes a los que accede desde sitios y bibliotecas de SharePoint. Si ya asignó permisos a los usuarios, dichos usuarios tendrán acceso a los elementos y las operaciones del servidor de informes inmediatamente después de configurarse la integración entre [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] y un servidor de informes. Puede usar los permisos existentes para cargar definiciones de informe y otros documentos, ver informes, crear suscripciones y administrar elementos.  
  
 Si no ha asignado permisos o si no está familiarizado con las características de seguridad de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], siga estas instrucciones:  
  
1.  En la documentación del producto para [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], lea la sección acerca de la configuración de seguridad predeterminada de los grupos estándar de SharePoint para obtener información acerca de cómo administrar los permisos y el acceso de usuario.  
  
2.  Revise la lista de permisos que afectan de forma específica a los elementos y las operaciones del servidor de informes. Para más información, vea [Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
3.  Asigne cuentas de usuario y de grupo a los grupos de SharePoint predefinidos.  
  
4.  Opcionalmente, cree niveles de permiso y grupos nuevos o modifique los existentes para variar los permisos de acceso al servidor según las necesidades aumentan.  
  
 Para usar las características de seguridad de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] con los elementos del servidor de informes, debe tener un servidor de informes que se ejecute en el modo integrado de SharePoint.  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>Acerca de los permisos, los niveles de permiso y los grupos de SharePoint  
 En la siguiente lista se proporciona una breve introducción a las características de seguridad de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]. Para obtener más información, vea la sección de Ayuda y procedimientos de Windows SharePoint en el sitio de SharePoint.  
  
-   Los objetos protegibles incluyen sitios, listas, bibliotecas, carpetas y documentos.  
  
-   Un permiso es una autorización para realizar una tarea específica. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] proporciona 33 permisos predefinidos que puede combinar en un nivel de permiso.  
  
-   Un nivel de permiso es un conjunto de permisos que se pueden conceder a los usuarios o a los grupos de SharePoint para un objeto protegible como un sitio, una biblioteca, una lista, una carpeta, un elemento o un documento. Equivale a una definición de roles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Existen cinco niveles de permiso predefinidos. Puede personalizarlos o crear otros nuevos si es necesario.  
  
-   Un grupo de SharePoint es un grupo de usuarios que se puede crear en un sitio de SharePoint para administrar los permisos del sitio y proporcionar una lista de distribución de correo electrónico para los miembros del sitio. Un grupo de SharePoint consta de cuentas de usuario y de grupo de Windows, o de inicios de sesión del usuario si usa la autenticación de formularios. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] proporciona tres grupos. Puede personalizarlos o crear otros nuevos si es necesario.  
  
-   La herencia de permisos permite que los subsitios, las listas y bibliotecas, y los elementos hereden la configuración de seguridad del sitio primario. Puede usar los permisos heredados para tener acceso a los elementos del servidor de informes almacenados en una biblioteca de SharePoint. El uso de la herencia de permisos y los grupos de SharePoint predefinidos puede simplificar la implementación y proporciona un acceso inmediato a la mayoría de las operaciones del servidor de informes.  
  
## <a name="who-sets-permissions"></a>Quién establece permisos  
 El administrador que instala [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], ejecuta el Asistente para configuración de SharePoint y crea el sitio del portal se convierte en el propietario del sitio del portal predeterminado El propietario del sitio puede establecer permisos en la Administración central para un conjunto de servidores o una aplicación web de SharePoint independiente, así como en el sitio de nivel superior de cada aplicación web de SharePoint. Además, dicha persona puede designar propietarios de sitios adicionales.  
  
 En el sitio de nivel superior de una aplicación web de SharePoint, los administradores de colecciones de sitios pueden establecer permisos para varios sitios en toda la jerarquía de sitios. Los propietarios de cada sitio pueden realizar las mismas tareas relacionadas con un subsitio.  
  
 Un administrador del servidor o de una colección de sitios puede establecer opciones que determinen si otros propietarios de sitios pueden establecer permisos. En función del nivel de permiso que tenga, es posible que no pueda crear o personalizar los grupos de SharePoint o los niveles de permiso.  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>Usar grupos de SharePoint y niveles de permiso predefinidos  
 En las recomendaciones de la documentación del producto de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] se recomienda usar los grupos estándar de SharePoint ( *Nombre del sitio* **Propietarios**, *Nombre del sitio* **Miembros**y *Nombre del sitio* **Visitantes**) y asignar permisos en el nivel de sitio. La mayoía de los usuarios a los que asigna permisos deben ser miembros de los grupos *Nombre del sitio* **Visitantes** o *Nombre del sitio* **Miembros** . Los permisos del sitio primario se heredan en toda la jerarquía de sitios. Puede anular la herencia de permisos para elementos específicos que requieran restricciones adicionales.  
  
 Los siguientes grupos de SharePoint tienen los siguientes niveles de permiso predefinidos:  
  
-   El grupo **Propietarios** tiene permisos de control total, lo que permite a los miembros del grupo realizar cambios en el contenido, las páginas o la funcionalidad del sitio. El acceso de control total debe estar limitado solamente a los administradores del sitio.  
  
-   El grupo **Miembros** tiene permisos del nivel Colaborar, lo que permite a los miembros del grupo ver páginas, editar elementos, enviar cambios para su aprobación, así como agregar y eliminar elementos de una lista.  
  
-   El grupo **Visitantes** tiene permisos del nivel de lectura, lo que permite a los miembros del grupo ver páginas, elementos de lista y documentos.  
  
 Los grupos de SharePoint tienen niveles de permiso que proporcionan un acceso inmediato a diversas operaciones del servidor de informes. Si la configuración de seguridad integrada no proporciona el nivel de acceso necesario, puede crear grupos o niveles de permiso personalizados.  
  
 Para más información sobre las operaciones del servidor de informes que son compatibles con las características de seguridad predeterminadas, vea [Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
 Para usar las características de seguridad integradas, debe asignar cuentas de usuario o de grupo de Windows a los grupos de SharePoint. Excepto en el caso del administrador del servidor y el propietario del sitio del portal, con acceso automático a [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] una vez instalado el software, se deben conceder permisos a los demás usuarios para que tengan acceso al servidor.  
  
## <a name="in-this-section"></a>En esta sección  
 [Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 Explica cómo se pueden usar los grupos de SharePoint y los niveles de permiso predefinidos para tener acceso a los elementos del servidor de informes.  
  
 [Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 Proporciona una referencia de todos los permisos de los productos de SharePoint que se pueden usar para tener acceso a las operaciones del servidor de informes.  
  
 [Establecer permisos para las operaciones del servidor de informes en una aplicación web de SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 Describe los requisitos de permisos de la notificación ad hoc y recomienda enfoques para que las características estén disponibles.  
  
 [Comparar roles y tareas de Reporting Services con grupos y permisos de SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 Proporciona un breve resumen de cómo comparar los grupos de SharePoint con las definiciones de roles predefinidas en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 Proporciona instrucciones para crear grupos de SharePoint nuevos con permiso para iniciar el Generador de informes y establecer la seguridad de elementos de modelo. En este tema también se incluyen instrucciones generales acerca de cómo establecer permisos personalizados para cualquier elemento u operación del servidor de informes.  
  
## <a name="see-also"></a>Ver también  
 [Seguridad y protección de Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
