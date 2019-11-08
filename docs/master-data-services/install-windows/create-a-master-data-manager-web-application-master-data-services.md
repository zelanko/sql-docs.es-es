---
title: Creación de una aplicación Web de Master Data Manager
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 384cf7989f41dce541afcfdd44b2831c79fde31e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729458"
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>Crear una aplicación web de Master Data Manager (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] proporciona una interfaz a los usuarios para trabajar con datos maestros y a los administradores para configurar y administrar MDS.  
  
 Una aplicación web debe estar siempre en un sitio web. Para crear una aplicación web, debe:  
  
-   Usar el sitio web predeterminado y volver a crear después la aplicación web,  
  
-   Utilizar un sitio web existente y luego crear la aplicación web, o  
  
-   Crear un nuevo sitio web que cree automáticamente una aplicación web.  
  
 Después de crear la aplicación web, debe asociarla a la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Para obtener información sobre los requisitos del equipo que hospeda la aplicación web, vea [Requisitos de la aplicación web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>Para crear una aplicación web de Master Data Manager en un sitio web nuevo  
 Cuando se crea un sitio web nuevo, la aplicación web raíz es la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . La aplicación web se agrega también a un nuevo grupo de aplicaciones.  
  
> [!NOTE]  
>  Si sigue este procedimiento, no podrá especificar una ruta de acceso virtual ni un alias de la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Si desea especificar una ruta de acceso virtual y un alias para [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], debe crear una aplicación web en un sitio web existente que aún no se haya configurado como una aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
 Además, [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] solo admite crear sitios con enlaces HTTP. Para agregar un enlace HTTPS, cree un sitio y una aplicación nuevos en [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] y después vea [Proteger una aplicación web Master Data Services](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md) para obtener más información.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>Para crear una aplicación web de Master Data Manager en un sitio web nuevo  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
3.  En la página **Configuración web** , en la lista Sitio web, seleccione **Crear sitio web**.  
  
4.  En el cuadro de diálogo **Crear sitio web** , especifique la información para un sitio web nuevo. Para obtener más información sobre las opciones de la interfaz de usuario (IU) en el cuadro de diálogo, vea [Cuadro de diálogo Crear sitio web &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>Para crear una aplicación web de Master Data Manager en un sitio web existente  
 Al crear una aplicación web en un sitio web existente , puede elegir la ruta de acceso virtual y el alias de la aplicación web. La aplicación web se agrega a un nuevo grupo de aplicaciones.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>Para crear una aplicación web de Master Data Manager en un sitio web existente  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
3.  En la página **Configuración web** , en la lista desplegable **Sitio web** , seleccione el sitio web en el que desea crear la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
4.  Haga clic en **Crear aplicación**.  
  
5.  En el cuadro de diálogo **Crear aplicación web** , especifique la información para una aplicación web nueva. Para obtener más información sobre las opciones de la interfaz de usuario (IU) en el cuadro de diálogo, vea [Cuadro de diálogo Crear aplicación web &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Asocie la aplicación web a una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Asociar una base de datos y una aplicación web de Master Data Services](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md).  
  
-   También puede configurar el sitio web en el que se hospeda la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] de forma que use un enlace HTTPS para cifrar el contenido con Capa de sockets seguros (SSL). Debe utilizar una herramienta de Internet Information Services (IIS), por ejemplo Administrador de IIS, para configurar el certificado de servidor para el servidor web y para configurar un enlace HTTPS y los parámetros de SSL para el sitio. Para más información, consulte [Secure a Master Data Manager Web Application](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md).  
  
## <a name="see-also"></a>Vea también  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
