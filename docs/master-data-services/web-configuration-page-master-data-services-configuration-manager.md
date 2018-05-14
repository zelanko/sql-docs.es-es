---
title: Página Configuración web (Administrador de configuración de Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a091986b14760632aff917967afef21e4e692898
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Página Configuración web (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use la página **Configuración web** para configurar un sitio web y una aplicación web. En ella también puede habilitar Data Quality Services  
  
## <a name="configure-the-web-application"></a>Configurar la aplicación web  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Sitio web**|Cree un nuevo sitio web, seleccione el sitio web predeterminado, o seleccione otro sitio disponible (si se muestra en la lista). Esta lista muestra los sitios web que se definen en Internet Information Services (IIS) en el equipo local. Cuando cree un nuevo sitio web, se creará automáticamente una aplicación web. Al seleccionar el valor predeterminado u otro sitio existente, debe crear una aplicación manualmente.|  
|**Aplicación web**|Seleccione una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para su configuración. Este cuadro muestra solamente las aplicaciones web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] en el sitio web seleccionado.<br /><br /> Si no se muestra nada, haga clic en **Crear** para crear un sitio web.|  
|**Crear**|Abre el cuadro de diálogo **Crear aplicación web** desde el que puede crear una aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] en el sitio seleccionado. Este botón se habilita solamente cuando el sitio seleccionado no tiene configurada ninguna aplicación web raíz como la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
  
## <a name="associate-application-with-database"></a>Asociar una aplicación con una base de datos  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Select**|Abre el cuadro de diálogo **Conectar con el servidor** desde el que podrá conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccionar una base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para asociarla con la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] seleccionada.|  
|**Instancia de SQL Server**|Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seleccionada que hospeda la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Este valor estará vacío hasta que se conecte a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione una base de datos.|  
|**Base de datos**|Muestra el nombre de la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que está asociada a la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] seleccionada. Este valor estará vacío hasta que se conecte a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccione una base de datos.|  
  
## <a name="enable-dqs-integration"></a>Habilitar integración con DQS  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Habilitar la integración con Data Quality Services**|Seleccione esta opción para habilitar la funcionalidad de Data Quality disponible en el [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Para obtener más información, consulte [Habilitar la integración de Data Quality Services con Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## <a name="see-also"></a>Ver también  
[Instalación y configuración de Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisitos de la aplicación web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
