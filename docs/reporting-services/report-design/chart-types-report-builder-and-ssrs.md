---
title: "Gráfico de tipos (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7b23da886ccf8fc76cbe8e86a722e4e9a8f3e656
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---

# <a name="chart-types-report-builder-and-ssrs"></a>Tipos de gráficos (Generador de informes y SSRS)

Es importante elegir el tipo de gráfico adecuado para el tipo de datos que se va a presentar. Esto determinará en qué medida se podrán interpretar correctamente los datos cuando se trasladen al gráfico. Por ejemplo, si el conjunto de datos contiene muchos puntos de datos expresados en relación con el tamaño del gráfico, es posible que resulte más adecuado presentarlos en un gráfico de áreas, de líneas o de dispersión. Para obtener más información sobre cómo preparar los datos en función del tipo de gráfico seleccionado, vea [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>Elegir un tipo de gráfico  
 Cada tipo de gráfico tiene características únicas para ayudarle a visualizar el conjunto de datos. Puede usar cualquier tipo de gráfico para mostrar los datos, pero éstos serán más fáciles de leer si elige un tipo de gráfico adecuado y basa su elección en lo que intenta mostrar en el informe. En la tabla siguiente se resumen las características de los gráficos que afectan a la idoneidad de un gráfico para un determinado conjunto de datos.  
  
 Puede cambiar el tipo de gráfico después de haberlo creado. Para obtener más información, vea [Cambiar un tipo de gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md).  
  
 Hay disponible ejemplos de muchos de estos tipos de gráficos como informes de ejemplo. Para obtener más información sobre cómo descargar los informes de ejemplo, vea [informes de ejemplo del generador de informes y el Diseñador de informes](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
|Tipo de gráfico|Muestra datos de proporción|Muestra datos de acciones|Muestra datos lineales|Muestra datos de varios valores|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[Gráficos de áreas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Gráficos de barras &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Barras de datos](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Gráficos de columnas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Gráficos de líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||||  
|[Gráficos polares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||||  
|[Rangos de intervalos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|  
|[Gráficos de dispersión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||  
|[Gráficos de formas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||||  
|[Minigráficos](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|  
|[Gráficos de cotizaciones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")||![Disponible](../../reporting-services/report-data/media/greencheck.gif "disponibles")|  

## <a name="next-steps"></a>Pasos siguientes

[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Puntos de datos en los gráficos vacíos y nulos](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[Agregar un gráfico a un informe](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
