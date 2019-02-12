---
title: Configurar la base de datos y el sitio Web de Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d2d2d034424ac4564a66b40b1479acb7dc683d7c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027186"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Configurar la base de datos y el sitio web para Master Data Services
  Use [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para configurar la base de datos y el sitio web para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS)  
  
 Para configurar la base de datos y el sitio web, realice las tareas siguientes.  
  
1.  Crear una base de datos mediante el **configuración de la base de datos** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Para obtener información, consulte [página de configuración de la base de datos &#40;Administrador de configuración de Master Data Services&#41; ](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) y [Asistente para crear base de datos &#40;Administrador de configuración de Master Data Services&#41; ](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  Crear un nuevo sitio Web, seleccione el sitio Web predeterminado o seleccione otro sitio Web existente, mediante el **configuración Web** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Luego, asocie la base de datos de MDS a la aplicación web que seleccione o cree.  
  
     Para obtener información, consulte [página configuración Web &#40;Administrador de configuración de Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) y [cuadro de diálogo Crear sitio Web &#40;Administrador de configuración de Master Data Services&#41; ](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  (Opcional) Habilitar la integración con Data Quality Services mediante el **configuración Web** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Para obtener más información, consulte [página configuración Web &#40;Administrador de configuración de Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) y [habilitar la integración de Data Quality Services con Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 También puede usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar la configuración de las aplicaciones web y los servicios asociados a la base de datos de MDS. Por ejemplo, puede especificar la frecuencia con la que se cargan los datos o con la que se envían correos electrónico de validación. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Base de datos de Master Data Services](../../2014/master-data-services/master-data-services-database.md)   
 [Aplicación web Master Data Manager](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
