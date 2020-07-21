---
title: Configurar la base de datos y el sitio web para Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d359084d1db778029046f925c630b001bb820f6b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971095"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Configurar la base de datos y el sitio web para Master Data Services
  Use [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para configurar la base de datos y el sitio web para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS)  
  
 Para configurar la base de datos y el sitio web, realice las tareas siguientes.  
  
1.  Cree una base de datos mediante la página **configuración de base de datos** en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] .  
  
     Para obtener más información, vea [página Configuración de base de datos &#40;administrador de configuración de Master Data Services](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) [Asistente para&#41;y crear base de datos &#40;administrador de configuración de Master Data Services ](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md)&#41;.  
  
2.  Cree un nuevo sitio web, seleccione el sitio web predeterminado o seleccione otro sitio web existente mediante la página **configuración Web** en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] . Luego, asocie la base de datos de MDS a la aplicación web que seleccione o cree.  
  
     Para obtener más información, vea [página Configuración Web &#40;administrador de configuración de Master Data Services](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) cuadro de diálogo&#41;y [crear sitio web &#40;administrador de configuración de Master Data Services ](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)&#41;.  
  
3.  Opta Habilite la integración con Data Quality Services mediante la página **configuración Web** en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] .  
  
     Para obtener más información, vea la [página Configuración Web &#40;Administrador de configuración de Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) y [Habilitar la integración de Data Quality Services con Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 También puede usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar la configuración de las aplicaciones web y los servicios asociados a la base de datos de MDS. Por ejemplo, puede especificar la frecuencia con la que se cargan los datos o con la que se envían correos electrónico de validación. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte también  
 [Master Data Services base de datos](../../2014/master-data-services/master-data-services-database.md)   
 [Aplicación web Master Data Services](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
