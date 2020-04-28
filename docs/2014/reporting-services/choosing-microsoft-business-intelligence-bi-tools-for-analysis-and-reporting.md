---
title: Análisis e informes con herramientas de Microsoft Business Intelligence (BI)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 7c76ec1a74032b5f35bc42ab4a901d95574e0900
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75688215"
---
# <a name="analysis-and-reporting-with-microsoft-business-intelligence-bi-tools"></a>Análisis e informes con herramientas de Microsoft Business Intelligence (BI)

  En la tabla siguiente se asignan las cargas de trabajo para el análisis de datos y los informes a las herramientas de Microsoft BI más adecuadas para esas cargas de trabajo.  
  
 La intención es ayudarle a elegir la herramienta que mejor satisface sus necesidades. Para obtener más información acerca de un producto, haga clic en el vínculo del producto en la tabla.  
  
 Si está buscando una breve introducción a estas herramientas para ayudarle a decidir cuáles son las adecuadas en su caso, vea [Introducing Microsoft Business Intelligence (BI) Tools](https://www.digitalvidya.com/blog/introduction-to-microsoft-power-bi/) [Introducción a las herramientas de Microsoft Business Intelligence (BI)].  
  
|Cargas de trabajo|Usuario|||Herramientas de BI|||  
|---------------|----------|-|-|--------------|-|-|  
|||**Excel**|**SharePoint**|**SharePoint Online**|**Power BI**|**SQL Server**|  
|**BI de autoservicio**|Analista o usuario final||||||  
|Detectar y acceder fácilmente a datos públicos y corporativos||[Power Query](https://go.microsoft.com/fwlink/p/?LinkId=391845)||[Azure Data Catalog](https://azure.microsoft.com/services/data-catalog/)<br /><br />||  
|Crear modelos de datos eficaces||[Power Pivot](https://support.office.com/article/power-pivot-overview-and-learning-f9001958-7901-4caa-ad80-028a6d2432ed?ui=en-US&rs=en-US&ad=US)|||[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)||  
|Realizar análisis predictivos de autoservicio||||||[Complementos de minería de datos para Excel](../analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins.md)|  
|Visualizar y explorar datos||[Power View](https://go.microsoft.com/fwlink/p/?LinkId=391847)<br /><br /> [Mapas 3D](https://support.office.com/article/visualize-your-data-in-3d-maps-ce6b1d5c-4602-4dae-b487-91ec0268e75d)|||||  
|Formular preguntas mediante consultas en lenguaje natural|||||[Q & A](https://docs.microsoft.com/power-bi/consumer/end-user-q-and-a)||  
|Acceder a informes mediante dispositivos móviles||||[HTML 5 (admite la visualización de archivos de <10 MB)](https://go.microsoft.com/fwlink/p/?LinkId=391853)|[HTML 5 (admite la visualización de <250 MB)](https://go.microsoft.com/fwlink/p/?LinkId=391854)<br /><br /> [Aplicación móvil de Power BI en dispositivos iOS](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-iphone-app-get-started)<br /><br /> [Aplicación móvil de Power BI en dispositivos Android](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-android-app-get-started) <br /><br />[Aplicación móvil de Power BI para Windows 10](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-windows-10-phone-app-get-started)||  
|Colaborar y compartir|||[Sitios de SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391849)|[Sitios de grupo de SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391850)|[Sitios de Power BI](https://docs.microsoft.com/power-bi/service-how-to-collaborate-distribute-dashboards-reports)||  
|**BI corporativo**|Profesional de TI||||||  
|Crear modelos corporativos multidimensionales/tabulares||||||[Analysis Services](https://docs.microsoft.com/analysis-services/analysis-services-overview)|  
|Crear visualizaciones de datos ad-hoc|||[Power View para SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391858)||||  
|Crear paneles|||[Paneles de SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391859)<br /><br /> [PerformancePoint Services](https://technet.microsoft.com/library/ee424392.aspx)||||  
|Crear informes operativos||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|Crear informes personalizados e incrustados||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|**Análisis avanzado**|Científico de datos||||||  
|Realizar análisis predictivos de autoservicio||||||[Complementos de minería de datos para Excel](https://msdn.microsoft.com/library/dn282385\(v=sql.120\).aspx)|  
|Usar algoritmos de minería de datos||||||[Minería de datos en Analysis Services](https://technet.microsoft.com/library/bb510516\(v=sql.120\).aspx)|  
  
 <sup>1</sup> Reporting Services tiene varias características que admiten la entrega de informes operativos e informes personalizados, como suscripciones y alertas de datos.