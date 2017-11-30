---
title: Agregar una referencia de ensamblado a un informe (SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
caps.latest.revision: "43"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c58d1678086858bf1aeda3998386805184f7c4b1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Agregar una referencia de ensamblado a un informe (SSRS)
  Al insertar código personalizado que contiene referencias a clases [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que no están en <xref:System.Math> ni en <xref:System.Convert>, necesita proporcionar una referencia de ensamblado al informe para que el procesador de informes pueda resolver los nombres. Para más información, vea [Agregar código a un informe &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Para agregar una referencia de ensamblado a un informe  
  
1.  En la vista **Diseño** , haga clic con el botón derecho en la superficie de diseño (fuera del borde del informe) y, después, haga clic en **Propiedades del informe**.  
  
2.  Haga clic en **Referencias**.  
  
3.  En **Agregar o quitar ensamblados**, haga clic en **Agregar** y, a continuación, haga clic en el botón de puntos suspensivos para buscar el ensamblado.  
  
4.  En **Agregar o quitar clases**, haga clic en **Agregar** y, a continuación, escriba el nombre de la clase y especifique un nombre de instancia para usarlo dentro del informe.  
  
    > [!NOTE]  
    >  Especifique un nombre de clase e instancia solo para miembros basados en instancias. No especifique miembros estáticos en la lista **Clases** . Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)subyacente.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Propiedades del informe (cuadro de diálogo), Referencias](http://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
