---
title: Combinaciones admitidas de SQL Server Reporting Services y SharePoint | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 10/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2e66cac836de44e8d2a9f23d88a600daaa26c0d1
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Combinaciones admitidas de SharePoint y el servidor de Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  Un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo de SharePoint requiere una versión de SharePoint y el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsSharePoint.msi) para productos de SharePoint, que se instalan en los servidores de SharePoint.  En este tema se resumen las combinaciones admitidas.  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinaciones admitidas de los componentes de Reporting Services y SharePoint  
 En la tabla siguiente se resumen las combinaciones admitidas de servidor de informes, complemento de Reporting Services para productos de SharePoint y productos de SharePoint. Las combinaciones que no se muestran en la tabla siguiente no se admiten  
  
### <a name="supported-combinations"></a>Combinaciones admitidas  
  
||Servidor de informes|Complemento|Versión de SharePoint|  
|-|-------------------|-------------|------------------------|  
|1|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2016|  
|2|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2013|  
|3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|  
|4|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|5|SQL Server 2012 SP3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y SQL Server 2012 SP3|SharePoint 2013|  
|6|SQL Server 2012 SP2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y SQL Server 2012 SP2|SharePoint 2013|  
|7|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|  
|8|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]*|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|9|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|  
|10|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|11|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|  
|12|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|  
|13|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
  
 *Excepción: no se admite la integración de Power View.  
  
 Para obtener vínculos a las páginas de descarga del complemento, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
 **Notas adicionales:**  

- Asegúrese de actualizar todos los servidores de SharePoint dentro de la granja de servidores. Esto incluye los servidores de front-end web y de aplicación.

-   La compatibilidad con SharePoint 2016, incluida la integración de Power View, requiere el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la versión del complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SQL Server 2016 o posterior.  

-   La compatibilidad con SharePoint 2013, incluida la integración de Power View, requiere el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la versión del complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SQL Server 2012 SP1 o posterior.  
  
-   Power View se presentó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Por tanto, la integración de Power View con SharePoint 2010 requiere la versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o posterior del complemento.  
  
-   Los servidores de informes de SQL Server 2012 (o posterior) no admiten el complemento de SQL Server 2008 R2. El instalador de requisitos previos de SharePoint 2010 instala automáticamente el complemento de SQL Server 2008 R2. Debe desinstalarse antes de instalar las versiones más recientes del complemento. No se admite la actualización en contexto del complemento.  
  
-   **Actualización:** SharePoint 2010 con el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no se puede actualizar en contexto a SharePoint 2013. SharePoint 2013 requiere la versión de [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior del complemento y el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información acerca de la actualización, vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  


