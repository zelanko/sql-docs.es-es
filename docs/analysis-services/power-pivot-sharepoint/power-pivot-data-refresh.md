---
title: "La actualización de datos dinámica de energía | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c5bc570e1f4f72fe932a8e5b2d0fa08c32f7949
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="power-pivot-data-refresh"></a>Actualización de datos PowerPivot
  Después de crear un libro que contiene datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede que desee actualizar los datos volviendo a ejecutar una consulta o comando periódicamente para conseguir información actualizada de los orígenes que se usaron originalmente para crear el libro. Este proceso se denomina **actualización de datos**y permite actualizar datos a petición en [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], o bien como una operación programada que se ejecuta como un proceso de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un servidor de aplicaciones de una granja de SharePoint. Para obtener más información, vea:  
  
-   [Actualización de datos Power Pivot con SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)  
  
-   [Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
-   [Configurar las credenciales almacenadas para la actualización de datos PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)  
  
-   [Programar una actualización de datos (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)  
  
-   [Ver el Historial de actualización de datos &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]y SharePoint Server 2013 Excel Services usan una arquitectura diferente para la actualización de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modelos de datos. La arquitectura admitida de SharePoint 2013 emplea Excel Services como componente principal para cargar modelos de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . La arquitectura usada anteriormente para la actualización de datos se basaba en un servidor que ejecutaba el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint para cargar los modelos de datos. Para obtener más información, vea:  
>   
>  -   [Actualización de datos Power Pivot con SharePoint 2013](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
