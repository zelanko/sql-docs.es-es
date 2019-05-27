---
title: Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05f0997cb73a156e54b22ad280fa5d6eb0ec7d73
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108648"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>Combinaciones admitidas del servidor y el complemento de SharePoint y Reporting Services (SQL Server 2014)
  Los servidores de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden instalarse en modo de SharePoint e integrarse con una implementación de SharePoint. No todas las características se admiten en todas las combinaciones de servidor de informes, complemento de Reporting Services para SharePoint y productos de SharePoint. En este tema se resumen las combinaciones admitidas. En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] la integración es el resultado de la combinación de las siguientes acciones:  
  
-   Una versión de un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para el modo de SharePoint.  
  
-   Un producto de SharePoint  
  
-   El complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint, que se instala en los servidores de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinaciones admitidas de los componentes de Reporting Services y SharePoint  
 En la tabla siguiente se resumen las combinaciones admitidas de servidor de informes, complemento de Reporting Services para productos de SharePoint y productos de SharePoint. Las combinaciones que no se muestran en la tabla siguiente no se admiten  
  
### <a name="supported-combinations"></a>Combinaciones admitidas  
  
||Servidor de informes|Complemento|Versión de SharePoint|Admitida|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|Sí|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sí|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|Sí|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sí<br /><br /> Excepción: No se admite la integración de Power view.|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|Sí|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sí|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|Sí|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|Sí|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sí|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|Sí|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sí|  
  
 Para obtener más información sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] características y los modos de servidor de informes, vea [Reporting Services Report Server](../reporting-services-report-server.md).  
  
 **Notas adicionales:**  
  
-   La compatibilidad con SharePoint 2013, incluida la integración de Power View, requiere el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la versión del complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SQL Server 2012 SP1 o posterior.  
  
-   Power View se presentó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Por tanto, la integración de Power View con SharePoint 2010 requiere la versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o posterior del complemento.  
  
-   Los servidores de informes de SQL Server 2012 (o posterior) no admiten el complemento de SQL Server 2008 R2. El instalador de requisitos previos de SharePoint 2010 instala automáticamente el complemento de SQL Server 2008 R2. Debe desinstalarse antes de instalar las versiones más recientes del complemento. No se admite la actualización en contexto del complemento.  
  
-   **Actualización:** SharePoint 2010 con el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento instalado, no se pueden actualizar en contexto a SharePoint 2013. SharePoint 2013 requiere la versión de [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o posterior del complemento y el servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información acerca de la actualización, vea [Upgrade and Migrate Reporting Services](upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Actualizar y migrar Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
