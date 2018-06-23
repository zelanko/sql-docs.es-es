---
title: Agregar un salto de página (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f9566d96747bc08636127f3bf350b4b9a121b847
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201093"
---
# <a name="add-a-page-break-report-builder-and-ssrs"></a>Agregar un salto de página (Generador de informes y SSRS)
  Puede agregar un salto de página a los rectángulos, las regiones de datos o los grupos situados dentro de las regiones de datos para controlar la cantidad de información de cada página. El hecho de agregar saltos de página puede mejorar el rendimiento de los informes publicados porque solo es necesario procesar los elementos de cada página para ver el informe. Cuando el informe entero está en una sola página, se deben procesar todos los elementos antes de poder verlo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-break-to-a-data-region"></a>Para agregar un salto de página a una región de datos  
  
1.  En la superficie de diseño, haga clic con el botón derecho en el controlador de tabla de la región de datos y luego haga clic en **Propiedades de Tablix**.  
  
2.  En la pestaña **General** , en **Opciones de salto de página**, seleccione una de las opciones siguientes:  
  
    -   **Agregar un salto de página antes**. Seleccione esta opción cuando desee agregar un salto de página antes de la tabla.  
  
    -   **Agregar un salto de página después**. Seleccione esta opción cuando desee agregar un salto de página después de la tabla.  
  
    -   **Ajustar la tabla a una sola página si es posible**. Seleccione esta opción cuando desee que los datos permanezcan en una página.  
  
### <a name="to-add-a-page-break-to-a-rectangle"></a>Para agregar un salto de página a un rectángulo  
  
1.  En la superficie de diseño, haga clic con el botón derecho en el rectángulo en que quiere agregar un salto de página y, luego, haga clic en **Propiedades del rectángulo**.  
  
2.  En la pestaña **General** , en **Opciones de salto de página**, seleccione una de las opciones siguientes:  
  
    -   **Agregar un salto de página antes**. Seleccione esta opción cuando desee agregar un salto de página antes del rectángulo.  
  
    -   **Agregar un salto de página después**. Seleccione esta opción cuando desee agregar un salto de página después del rectángulo.  
  
    -   **Omitir borde en el salto de página**. Seleccione esta opción cuando no desee un borde en el salto de página.  
  
    -   **Mantener el contenido en una sola página, si es posible**. Seleccione esta opción si desea que el contenido del rectángulo permanezca en una página.  
  
### <a name="to-add-a-page-break-to-a-row-group-in-a-table-matrix-or-list"></a>Para agregar un salto de página a un grupo de filas de una tabla, una matriz o una lista  
  
1.  En el panel Agrupación, haga clic con el botón derecho en un grupo de filas y, luego, haga clic en **Propiedades de grupo**.  
  
    > [!NOTE]  
    >  Los saltos de página se omiten en los grupos de columnas.  
  
2.  En la pestaña **Saltos de página** , seleccione **Entre cada instancia de un grupo** para agregar un salto de página entre cada instancia de un grupo de la tabla.  
  
3.  Opcionalmente, seleccione **También al principio de un grupo** o **También al final de un grupo** para especificar que se agregue un salto de página cuando un grupo se inicie o finalice en la tabla.  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [Encabezados y pies de página &#40;el generador de informes SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)  
  
  