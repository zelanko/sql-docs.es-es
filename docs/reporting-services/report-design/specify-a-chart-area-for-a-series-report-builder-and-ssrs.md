---
title: "Especificar un área del gráfico para una serie (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10157"
- sql13.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d88358516e05214b230ec57b6243168ef9aac048
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>Especificar un área de gráfico para una serie (Generador de informes y SSRS)
  En los informes paginados de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , el *gráfico* es el contenedor de nivel superior que incluye el borde exterior, el título del gráfico y la leyenda. De manera predeterminada, el gráfico contiene un *área de gráfico*. El área de gráfico no está visible en la superficie del gráfico, pero puede imaginarla como un contenedor que incluye únicamente las etiquetas del eje, el título del eje y el área de trazado de una o más series. En la ilustración siguiente se muestra el concepto de varias áreas de gráfico dentro de un único gráfico.  
  
 ![Muestra un diagrama de un área del gráfico](../../reporting-services/report-design/media/chartareasdiagram.gif "muestra un diagrama de un área del gráfico")  
  
 De forma predeterminada, todas las series se agregan al área de gráfico predeterminada. Cuando se usan gráficos de áreas, de columnas, de líneas y de dispersión, cualquier combinación de estas series se puede mostrar en la misma área de gráfico. Si tiene varias series en la misma área de gráfico, se reducirá la legibilidad del gráfico. Es recomendable separar los tipos de gráfico en varias áreas de gráfico. El uso de varias áreas de gráfico aumentará la legibilidad, facilitando las comparaciones. Por ejemplo, los gráficos de cotizaciones de volumen y precios suelen tener intervalos de valores diferentes, pero se pueden realizar comparaciones entre los datos de volumen y de precio durante el mismo período de tiempo.  
  
 Las series de tipo barras, polar o de formas solo se pueden combinar con series de los mismos tipos de gráfico en la misma área de gráfico. Si usa un gráfico polar o de formas, considere la posibilidad de usar una región de datos independiente para cada campo que desee mostrar.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-associate-a-series-with-a-new-chart-area"></a>Para asociar una serie a una nueva área de gráfico  
  
1.  Haga clic con el botón derecho en cualquier lugar del gráfico y seleccione **Agregar una nueva área de gráfico**. Aparecerá una nueva área de gráfico en blanco en el gráfico.  
  
2.  Haga clic con el botón derecho en la serie del gráfico o en un campo de serie o de datos en la zona apropiada del panel Datos del gráfico y, después, haga clic en **Propiedades de la serie**.  
  
3.  En **Ejes y área del gráfico**, seleccione el área de gráfico en la que desea mostrar la serie.  
  
4.  (Opcional) Alinee verticalmente las áreas de gráfico. Para ello, haga clic con el botón derecho en el gráfico y seleccione **Propiedades del área de gráfico**. En **Alineación**, seleccione el área de gráfico con la que desea alinear el área de gráfico seleccionada.  
  
## <a name="see-also"></a>Vea también  
 [Mostrar varias Series en un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a los puntos de datos en un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Definir los colores de un gráfico mediante una paleta &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Los gráficos polares &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)   
 [Gráficos de formas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [Los gráficos circulares &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
