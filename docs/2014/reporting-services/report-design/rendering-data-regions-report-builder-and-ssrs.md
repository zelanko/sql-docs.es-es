---
title: Representar regiones de datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 918aa5eee3aada465e904cf7f1627f93d1b9bb6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105368"
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>Representar regiones de datos (Generador de informes y SSRS)
  Además de los comportamientos generales de representación que se aplican a todos los elementos de informe, las regiones de datos están sujetas a comportamientos de paginación y de representación adicionales. Las reglas de representación específicas de las regiones de datos describen la forma en la que crece una región de datos, cómo se representan las celdas especiales, como la celda de la esquina o las celdas de encabezado, y cómo se representa una región de datos para la lectura de derecha a izquierda. En este tema se explica cómo se representan las distintas partes de una región de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Regiones de datos Tablix  
 La región de datos Tablix, que permite crear tablas, matrices y listas, se representa como una cuadrícula formada por columnas y filas. La intersección de una fila y una columna es una celda. Cuando se representa, esta celda puede contener datos u otros elementos de informe, como imágenes, rectángulos, cuadros de texto o subinformes. Una región de datos Tablix puede crecer tanto vertical como horizontalmente. Además, la celda de la esquina, las celdas de encabezado de la región de datos y las celdas del cuerpo de la región de datos pueden crecer en función de su contenido. Si la región de datos ocupa varias páginas, los elementos de informe configurados para que se repitan con la región de datos se representan en cada una de las páginas en las que se muestra ésta. Para obtener más información, consulte [enumera &#40;generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="right-to-left"></a>De derecha a izquierda  
 Una región de datos Tablix que se haya configurado para mostrarse de derecha a izquierda se representa con su estructura como una imagen reflejada de la región de datos tal como se representaría de izquierda a derecha. La esquina de la región de datos aparece en la esquina superior derecha. Si el informe incluye columnas dinámicas, éstas se expanden hacia la izquierda. La configuración de derecha a izquierda no afecta al orden de los datos en la región de datos; simplemente, las columnas se ordenan de forma diferente.  
  
### <a name="tablix-headers"></a>Encabezados del Tablix  
 Los encabezados del Tablix se representan como un encabezado de fila o un encabezado de columna dependiendo de dónde aparece la celda de encabezado en la jerarquía del grupo de filas o del grupo de columnas. Si el contenido de la celda de un encabezado incluye un salto de página lógico, éste se omite. Los saltos de página lógicos en los grupos de columnas se omiten.  
  
 Los saltos de página lógicos en los grupos no ocasionan la ruptura de los encabezados de grupo externos. Por ejemplo, imagine que el informe tiene un grupo externo de país y un grupo interno de región del país. Si existe un salto de página lógico entre las instancias del grupo de región del país, el grupo exterior, el país, aparecerá en ambas páginas del informe.  
  
#### <a name="repeated-tablix-headers"></a>Encabezados del Tablix repetidos  
 Cuando se establece la propiedad RepeatWith en el panel **Propiedades** , los elementos que no cambian dentro de la región de datos, como los encabezados de columna, se repiten en cada una de las páginas en las que se representa esa parte de la región de datos. Por ejemplo, si una fila de datos aparece en la página siguiente y se establece la propiedad Repeat With, los encabezados de columna también aparecerán en la página representada.  
  
### <a name="tablix-corner"></a>Esquina de Tablix  
 La esquina superior izquierda es la que se denomina esquina de Tablix. La esquina de Tablix puede contener otros elementos de informe pero, si se insertan saltos de página lógicos en la esquina, éstos se omitirán al representar la región de datos Tablix.  
  
### <a name="tablix-body"></a>Cuerpo del Tablix  
 El cuerpo del Tablix se compone de las celdas de Tablix. El cuerpo del Tablix se representa teniendo en cuenta las reglas de paginación y los comportamientos de representación de los elementos de informe. Para obtener más información, vea [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md).  
  
## <a name="chart-gauge-and-map-data-regions"></a>Regiones de datos Gráfico, Medidor y Mapa  
 Las regiones de datos Gráfico, Medidor y Mapa se comportan como imágenes cuando se representan y se muestran en el cuerpo del informe. Los valores existentes dentro de la región de datos pueden tener acciones asociadas, como vincularse con otro informe o desplazarse a un marcador, y éstas acciones también se pueden representar, si el representador lo admite.  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
