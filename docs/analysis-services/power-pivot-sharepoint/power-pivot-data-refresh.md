---
title: Actualización de datos PowerPivot de energía | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 243c2649af82aad3488051da543628203699a27e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201756"
---
# <a name="power-pivot-data-refresh"></a>Actualización de datos PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Después de crear un libro que contiene datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede que desee actualizar los datos volviendo a ejecutar una consulta o comando periódicamente para conseguir información actualizada de los orígenes que se usaron originalmente para crear el libro. Este proceso se denomina **actualización de datos**y permite actualizar datos a petición en [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], o bien como una operación programada que se ejecuta como un proceso de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un servidor de aplicaciones de una granja de SharePoint. Para obtener más información, vea:  
  
-   [Actualización de datos Power Pivot con SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)  
  
-   [Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
-   [Configurar las credenciales almacenadas para la actualización de datos PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)  
  
-   [Programar una actualización de datos (Power Pivot para SharePoint)](http://msdn.microsoft.com/8571208f-6aae-4058-83c6-9f916f5e2f9b)  
  
-   [Ver el Historial de actualización de datos &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y SharePoint Server 2013 Excel Services usan una arquitectura diferente para la actualización de datos de modelos de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . La arquitectura admitida de SharePoint 2013 emplea Excel Services como componente principal para cargar modelos de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . La arquitectura usada anteriormente para la actualización de datos se basaba en un servidor que ejecutaba el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint para cargar los modelos de datos. Para obtener más información, vea:  
> 
>  -   [Actualización de datos Power Pivot con SharePoint 2013](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
