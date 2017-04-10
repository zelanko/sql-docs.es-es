---
title: "No se puede cargar el archivo o ensamblado &#39;Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089&#39; ni una de sus dependencias. El sistema no encuentra el archivo especificado. | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# No se puede cargar el archivo o ensamblado &#39;Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089&#39; ni una de sus dependencias. El sistema no encuentra el archivo especificado.
  En entornos de SharePoint 2010 que tienen PowerPivot para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este error se producirá si intenta realizar la exportación de una fuente de distribución de datos y el sistema no tiene la versión necesaria de Microsoft ADO.NET Data Services.  
  
## Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|No se encontró ADO.NET Data Services 3.5 SP1.|  
|Texto del mensaje|No se puede cargar el archivo o ensamblado 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ni una de sus dependencias. El sistema no encuentra el archivo especificado.|  
  
## Explicación  
 SharePoint 2010 incluye un botón Exportar como fuente de distribución de datos que puede utilizar para exportar una lista de SharePoint como una fuente de distribución de datos XML. Además, tanto Reporting Services en el modo de SharePoint como [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint admiten las características de fuentes de distribución de datos que requieren ADO.NET Data Services.  
  
 Si no está instalado ADO.NET Data Services, este error se producirá al solicitar una fuente de distribución de datos.  
  
## Acción del usuario  
  
1.  Vaya a la documentación sobre los requisitos de hardware y software de SharePoint 2010, [Requisitos de hardware y software (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  En **Instalar requisitos previos de software**, busque el vínculo de ADO.NET Data Services 3.5 correspondiente al sistema operativo que está usando.  
  
3.  Haga clic en el vínculo y ejecute el programa de instalación que instala el servicio.  
  
## Vea también  
 [Implementar las soluciones de Power Pivot en SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  