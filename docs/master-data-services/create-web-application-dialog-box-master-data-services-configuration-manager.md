---
title: "Cuadro de diálogo Crear aplicación web (Administrador de configuración de Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3cd75c85b6319d2211676b694066a2acf2c8002c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>Cuadro de diálogo Crear aplicación web (Administrador de configuración de Master Data Services)
  Utilice el cuadro de diálogo **Crear aplicación web** para crear la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esta aplicación web se crea en el sitio que seleccionó en la página **Configuración web** .  
  
## <a name="web-application"></a>Aplicación web  
 El servidor web sirve el contenido para esta aplicación web desde la carpeta [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **de** en el sistema de archivos. Esta ubicación se especifica durante la instalación y, de manera predeterminada, la ruta de acceso es *unidad*:\Archivos de programa\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|Ruta de acceso virtual|Seleccione la ruta de acceso virtual en la que desea crear la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Una ruta de acceso virtual forma parte de la dirección URL que se utiliza para tener acceso a una aplicación web.<br /><br /> Esta lista se filtra solo para mostrar rutas de acceso virtual de aplicaciones en las que se puede crear la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . No puede crear una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] en otra aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
|Alias|Escriba un nombre para la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o use el nombre predeterminado. Este nombre se utiliza en una dirección URL para tener acceso a la aplicación web de un explorador web.|  
  
## <a name="application-pool"></a>Grupo de aplicaciones  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Nombre**|Escriba un nombre descriptivo único para un nuevo grupo de aplicaciones o bien utilice el nombre predeterminado. La aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] se agrega a este grupo de aplicaciones.<br /><br /> Los grupos de aplicaciones proporcionan límites que evitan que las aplicaciones en un grupo de aplicaciones afecten a las aplicaciones en otro grupo de aplicaciones.|  
|**Nombre de usuario.**|Especifique un dominio y nombre de usuario en Active Directory. Esta cuenta es la identidad del grupo de aplicaciones donde se ejecuta la aplicación web. Esta cuenta debe ser la misma que se especificó como cuenta de servicio cuando se creó la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Esta cuenta se agrega al rol de base de datos mds_exec de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para el acceso a la base de datos. Para obtener más información, vea [Inicios de sesión, usuarios y roles en bases de datos &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). También se agrega a un grupo de Windows de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], **MDS_ServiceAccounts**, al que se le concede permiso al directorio de compilación temporal, **MDSTempDir**, en el sistema de archivos. Para obtener más información, vea [Permisos de carpetas y archivos&#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Contraseña**|Escriba la contraseña de la cuenta de usuario especificada.|  
|**Confirmar contraseña**|Vuelva a escribir la contraseña de la cuenta de usuario especificada. Los campos **Contraseña** y **Confirmar contraseña** deben contener la misma contraseña.|  
  
## <a name="see-also"></a>Vea también  
 [Página Configuración web &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Instalación y configuración de Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisitos de la aplicación web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
