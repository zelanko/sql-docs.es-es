---
title: Cambiar el orden de un parámetro de informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef2d2fd7455b3757dcbdc7eb1d60e95b2f8fc664
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>Cambiar el orden de un parámetro de informe (Generador de informes y SSRS)
  Cambie el orden de los parámetros de informe cuando tenga un parámetro dependiente que aparece antes que el parámetro del que depende. El orden de los parámetros es importante cuando se tienen parámetros en cascada, o cuando se desea mostrar a los usuarios el valor predeterminado de un parámetro antes de que elijan valores para otros parámetros. Un parámetro de informe dependiente contiene una referencia, ya sea en su consulta de valores predeterminados o en su consulta de valores válidos, a un parámetro de consulta que señala a un parámetro de informe situado después de él en la lista de parámetros del panel **Datos de informe** .  
  
 El orden en que se ven los parámetros en la barra de herramientas del visor de informes al ejecutar el informe lo determina el orden de los parámetros del panel **Datos de informe** y la ubicación de los parámetros del panel de parámetros personalizado. Para más información, vea [Customize the Parameters Pane in a Report &#40;Report Builder&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md) (Personalizar el panel de parámetros en un informe [Generador de informes]).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>Para cambiar el orden de los parámetros de informe  
  
Para cambiar el orden de los parámetros de informe, realice alguna de las acciones siguientes:  
  
-   Haga clic en un parámetro en el panel **Datos de informe** y use los botones de flecha arriba y flecha abajo para mover el parámetro hacia arriba o hacia abajo en la lista, como se muestra en la imagen siguiente.  Cuando cambia el orden del parámetro en el panel **Datos de informe** , también cambia la ubicación del parámetro en el panel de parámetros.  
  
     ![Cambiar el orden de los parámetros en el panel Datos de informe](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "Cambiar el orden de los parámetros en el panel Datos de informe")  
  
-   En el panel de parámetros, arrastre el parámetro a una nueva columna o fila del panel. Al cambiar la ubicación del parámetro en el panel, también cambia el orden de los parámetros en el panel **Datos de informe** . Para más información sobre cómo mover los parámetros en el panel, vea [Customize the Parameters Pane in a Report &#40;Report Builder&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md) (Personalizar el panel de parámetros en un informe [Generador de informes]).  
  
## <a name="see-also"></a>Ver también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
