---
title: Agregar HTML a un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e799ac6b1c633b3374a80e156a9ba6ce51aaac9a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Agregar HTML a un informe (Generador de informes y SSRS)
  Mediante un marcador de posición, puede importar HTML de un campo del conjunto de datos para usarlo en el informe. De forma predeterminada, un marcador de posición representa texto simple, por lo que deberá cambiar el tipo de marcado del marcador de posición a HTML. Para más información, vea [Importar HTML en un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>Para agregar HTML de un campo del conjunto de datos en un cuadro de texto  
  
1.  En la pestaña **Insertar** , haga clic en **Lista**. Haga clic en la superficie de diseño y, a continuación, arrastre para crear un cuadro que tenga el tamaño que desee.  
  
     Se abre el cuadro de diálogo **Propiedades del conjunto de datos** . En el informe, podrá utilizar un conjunto de datos compartido o un conjunto de datos incrustado. Para más información, haga clic en [Propiedades del conjunto de datos (cuadro de diálogo), Consulta &#40;Generador de informes&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) o [Propiedades del conjunto de datos (cuadro de diálogo), Consulta](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f).  
  
2.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**. Haga clic en la lista y, a continuación, arrastre para crear un cuadro que tenga el tamaño que desee.  
  
3.  Arrastre un campo HTML desde el conjunto de datos hasta el cuadro de texto. Se crea un marcador de posición para el campo.  
  
4.  Haga clic con el botón derecho en el marcador de posición y, después, haga clic en **Propiedades de marcador de posición**.  
  
5.  En la pestaña **General** , compruebe que el cuadro **Valor** contiene una expresión que se evalúa como el campo que colocó en el paso 3.  
  
6.  Haga clic en **HTML - Interpretar etiquetas HTML como estilos**. Esto provocará que el campo se evalúe como HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a números y fechas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Aplicar formato a líneas, colores e imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Cuadro de diálogo Propiedades del marcador de posición, General &#40;Generador de informes y SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
