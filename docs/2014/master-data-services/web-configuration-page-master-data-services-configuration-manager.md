---
title: Página Configuración web (Administrador de configuración de Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 12ba4a2d03e98d5f2dac79917e23a93c0a24cdb0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481209"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Página Configuración web (Master Data Services)
  Use la página **Configuración web** para crear un nuevo sitio web o una aplicación web. Una vez haya seleccionado una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , puede especificar la base de datos de la aplicación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] y habilitar Data Quality Services.  
  
## <a name="configure-the-web-application"></a>Configurar la aplicación web  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Bsitio**|Cree un nuevo sitio web, seleccione el sitio web predeterminado, o seleccione otro sitio disponible (si se muestra en la lista). Esta lista muestra los sitios web que se definen en Internet Information Services (IIS) en el equipo local. Cuando cree un nuevo sitio web, se creará automáticamente una aplicación web. Al seleccionar el valor predeterminado u otro sitio existente, debe crear una aplicación manualmente.|  
|**Aplicación web**|Seleccione una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para su configuración. Este cuadro muestra solamente las aplicaciones web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] en el sitio web seleccionado.<br /><br /> Si no se muestra nada, haga clic en **Crear aplicación** para crear un sitio web.|  
|**Create Application (Crear aplicación)**|Abre el cuadro de diálogo **Crear aplicación web** desde el que puede crear una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] en el sitio seleccionado. Este botón se habilita solamente cuando el sitio seleccionado no tiene configurada ninguna aplicación web raíz como la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
  
## <a name="associate-application-with-database"></a>Asociar una aplicación con una base de datos  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**No**|Abre el cuadro de diálogo **Conectar con el servidor** desde el que podrá conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccionar una base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para asociarla con la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] seleccionada.|  
|**Instancia de SQL Server**|Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seleccionada que hospeda la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Este valor estará vacío hasta que se conecte a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione una base de datos.|  
|**Base de datos**|Muestra el nombre de la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que está asociada a la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] seleccionada. Este valor estará vacío hasta que se conecte a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione una base de datos.|  
  
## <a name="enable-dqs-integration"></a>Habilitar integración con DQS  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Habilitación de la integración con Data Quality Services**|Seleccione esta opción para habilitar la funcionalidad de Data Quality disponible en el [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Para obtener más información, consulte [Habilitar la integración de Data Quality Services con Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la base de datos y el sitio web para Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisitos de la aplicación web &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [Cree una aplicación Web de Master Data Manager &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [MDS 2014 y el error "servicio no disponible"](https://blogs.msdn.com/b/womeninanalytics/archive/2015/08/19/mds-2014-and-service-unavailable-error.aspx)  
  
  
