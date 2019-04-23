---
title: Comparar funciones de inteligencia empresarial en diferentes entornos de Microsoft | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 13ae9380cc3f034ace5f43d83640eea665cb3b02
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944611"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Comparar funciones de Business Intelligence en diferentes entornos de Microsoft

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence se puede implementar en varios entornos diferentes, incluido [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SharePoint Server, SharePoint Online y Power BI para Office 365. En este tema se comparan los componentes y las características compatibles en cada entorno.  
  
Para obtener más información comparando SharePoint Server y SharePoint Online, consulte [Comparar planes y opciones de SharePoint](http://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Crear y administrar paneles e informes de BI  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Plan 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Sitios BI|Galería de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]|No|Sitio de Power BI|  
|Centralización de datos y uso compartido y administración de datos|No|No|Sí **<sup>1</sup>**|  
|Integración con Master Data Services (MDS) and Data Quality Services (DQS)|Sí|No|No|  
|Programar actualizaciones de datos|Sí, pero no ofrece compatibilidad para libros que contienen datos de Power Query|No|Sí|  
|Consultas en lenguaje natural (preguntas y respuestas)|No|No|Sí **<sup>2</sup>**|  
|Previsión de predicción|No|No|Sí **<sup>3</sup>**|  
|Integración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sí|No|No|  
|Integración de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (multidimensional y tabular)|Sí|No|No|  
|Exportar el panel interactivo de Power View a presentación de PowerPoint|Sí|No|No|  
|Creación del panel en el explorador|Sí|No|No|  
|Supervisión de la utilización|Sí|No|Sí|  
|Aprovechamiento de seguridad basada en filas de cubos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Sí|No|No|  
  
 **<sup>1</sup>**[descripción del rol de administradores de datos de administración de datos](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) y [vídeo: Administración de información de BI y centralización de datos de energía](https://www.youtube.com/watch?v=8dHOj68ts7c).  
  
 **<sup>2</sup>**[power BI Q & A: Optimizar un libro de Power BI (modelado en la nube)](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/).  
  
 **<sup>3</sup>**[introducir nuevas funciones de previsión en Power View para Office 365](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Vea y explore datos de BI, informes y paneles.  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Plan 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Vea libros de Microsoft Excel en un explorador.|Sí, si el tamaño del libro es inferior a 2 GB|Sí, si el tamaño del libro es inferior a 10 MB|Sí, si el tamaño del libro es inferior a 250 MB|  
|Exploración de datos en el explorador en HTML5|No|No|Sí|  
|Aplicación de BI para móviles para acceder a informes y paneles de forma remota|No|No|Sí **<sup>1</sup>**|  
|Libro de Excel con [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como origen de datos **<sup>2</sup>**|Sí|No|No|  
|Capacidad para usar las funciones en distintos exploradores y versiones|Sí, para las visualizaciones que no sean en Power View **<sup>3</sup>**|Sí, tamaños de archivos de libros inferiores a 10 MB **<sup>3</sup>**|Sí **<sup>3</sup>**|  
  
 **<sup>1</sup>**  [Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).  
  
 **<sup>2</sup>**  [Libros de PowerPivot como origen de datos](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [Compatibilidad con dispositivos móviles en todas las herramientas de Business Intelligence (BI)](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) y [planeación de la compatibilidad del explorador de Reporting Services y Power View (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx).  
  
## <a name="more-information"></a>Más información  
  
- [Capacidades BI en Excel y Office 365](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743).  
  
- Para obtener información sobre los requisitos para poder usar sinónimos, vea [optimizar Power BI preguntas y respuestas con sinónimos & frases](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling) en pragmaticworks.com.  
  
- [Office Online, elija su red social empresarial: ¿Yammer o Newsfeed? ](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Power BI para Office 365](https://www.microsoft.com/powerbi/default.aspx).  
  
- [Precios de Power BI](https://www.microsoft.com/powerBI/pricing.aspx).  
  
- [Análisis e informes con las herramientas de Microsoft business intelligence (BI)](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>Contenido de la comunidad

[BI de autoservicio de Microsoft local frente a la nube](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/).