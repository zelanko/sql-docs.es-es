---
title: Comparar funciones de inteligencia empresarial en diferentes entornos de Microsoft | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fb759ee-8172-4c4c-9f7d-49af2c731006
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: ae54486aa141880189a012d897251604a292aefe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201336"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Comparar funciones de Business Intelligence en diferentes entornos de Microsoft
  Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence se puede implementar en varios entornos diferentes, incluidos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con SharePoint Server, SharePoint Online y Power BI para Office 365. En este tema se comparan los componentes y las características compatibles en cada entorno.  
  
 Para obtener más información comparando SharePoint Server y SharePoint Online, consulte [Comparar planes y opciones de SharePoint](http://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Crear y administrar paneles e informes de BI  
  
||SQL Server 2014 y SharePoint Server 2013|SharePoint Online Plan 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Sitios BI|Galería de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]|no|Sitio de Power BI|  
|Centralización de datos y uso compartido y administración de datos|no|no|Sí  **<sup>1</sup>**|  
|Integración con Master Data Services (MDS) and Data Quality Services (DQS)|Sí|no|no|  
|Programar actualizaciones de datos|Sí, pero no ofrece compatibilidad para libros que contienen datos de Power Query|no|Sí|  
|Consulta en lenguaje natural (Q&A)|no|no|Sí  **<sup>2</sup>**|  
|Previsión de predicción|no|no|Sí  **<sup>3</sup>**|  
|Integración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sí|no|no|  
|Integración de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (multidimensional y tabular)|Sí|no|no|  
|Exportar el panel interactivo de Power View a presentación de PowerPoint|Sí|no|no|  
|Creación del panel en el explorador|Sí|no|no|  
|Supervisión de la utilización|Sí|no|Sí|  
|Aprovechamiento de seguridad basada en filas de cubos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Sí|no|no|  
  
 **<sup>1</sup>**[descripción del rol de administradores de datos de administración de datos](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) y [vídeo: administración de información de BI y centralización de datos de energía](https://www.youtube.com/watch?v=8dHOj68ts7c).    
  
 **<sup>2</sup>**[power BI preguntas y respuestas: optimizar un libro de Power BI (modelado en la nube)](https://support.office.com/article/Power-BI-Q-A-Optimize-a-Power-BI-workbook-cloud-modeling--96dc5941-d0f1-44e2-9d9d-c038a3a55849?ui=en-US&rs=en-US&ad=US).    
  
 **<sup>3</sup>**[introducir nuevas funciones de previsión en Power View para Office 365](http://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).    
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Vea y explore datos de BI, informes y paneles.  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Plan 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Vea libros de Microsoft Excel en un explorador.|Sí, si el tamaño del libro es inferior a 2 GB|Sí, si el tamaño del libro es inferior a 10 MB|Sí, si el tamaño del libro es inferior a 250 MB|  
|Exploración de datos en el explorador en HTML5|no|no|Sí|  
|Aplicación de BI para móviles para acceder a informes y paneles de forma remota|no|no|Sí  **<sup>1</sup>**|  
|Libro de Excel con [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como un origen de datos  **<sup>2</sup>**|Sí|no|no|  
|Capacidad para usar las funciones en distintos exploradores y versiones|Sí, para las visualizaciones no Power View  **<sup>3</sup>**|Sí, libro tamaños de archivos de menos de 10 MB  **<sup>3</sup>**|Sí  **<sup>3</sup>**|  
  
 **<sup>1</sup>**[Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).    
  
 **<sup>2</sup>**[libros PowerPivot como origen de datos  ](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**[compatibilidad con dispositivos móvil a través de herramientas de Business Intelligence (BI)](http://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) y [planeamiento para Reporting Services y compatibilidad con explorador de Power View (Reporting Services 2014)](http://msdn.microsoft.com/library/ms156511.aspx).    
  
## <a name="more-information"></a>Más información  
  
-   [Capacidades de inteligencia empresarial en Excel, SharePoint Online y Power BI para Office 365](https://technet.microsoft.com/en-us/library/dn198235.aspx).  
  
-   Para obtener información sobre los requisitos para poder usar sinónimos, consulte [Agregar sinónimos a un modelo de datos de Excel de Power Pivot](https://support.office.com/Article/Add-synonyms-to-a-Power-Pivot-Excel-data-model-345f4f5b-5ec2-4998-bc46-a26bdc0810b6?ui=en-US&rs=en-US&ad=US).  
  
-   [Office Online, elija su red social empresarial: ¿Yammer o Newsfeed?](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
-   [Power BI para Office 365](http://www.microsoft.com/powerbi/default.aspx).  
  
-   [Precios de Power BI](http://www.microsoft.com/powerBI/pricing.aspx).  
  
-   [Comparar un sitio del centro de BI con sitios de Power BI para Office 365](http://technet.microsoft.com/library/dn394343\(v=office.15\).aspx).  
  
-   [Introducción a herramientas de análisis e informes de BI de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=617093)  
  
## <a name="community-content"></a>Contenido de la comunidad  
 [BI de autoservicio de Microsoft local frente a la nube](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/).  
  
  