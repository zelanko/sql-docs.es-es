---
title: Referencias a la colección ReportItems (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0779913a4334a1142c8a5c8d7561aaa9ecd980cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>Colecciones integradas: referencias a la colección ReportItems (Generador de informes)
  La colección integrada **ReportItems** es el conjunto de los cuadros de texto de los elementos de informe, como las filas de una región de datos o los cuadros de texto de la superficie de diseño del informe. La colección **ReportItems** incluye los cuadros de texto que están en el ámbito actual de un encabezado de página, un pie de página o el cuerpo del informe. Esta colección la determinan en tiempo de ejecución el procesador de informes y el representador de informes. El ámbito actual va cambiando mientras el procesador de informes va combinando consecutivamente los datos del informe y los elementos de diseño de los elementos del informe a medida que el usuario visualiza las páginas de un informe. Puede usar la colección integrada **ReportItems** para generar encabezados de página de estilo diccionario que muestren el primer y el último elemento de cada página.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>Usar la propiedad Value de ReportItems  
 Los elementos de la colección **ReportItems** solo tienen una propiedad: Value. El valor de un elemento de **ReportItems** puede usarse para mostrar o calcular datos de otro campo del informe. Para acceder al valor del cuadro de texto actual, puede usar el valor global integrado Me.Value o simplemente Value de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . En las funciones de informe, como First y las funciones de agregado, use la sintaxis completa.  
  
 Por ejemplo:  
  
-   Esta expresión, ubicada en un cuadro de texto, muestra el valor de un cuadro de texto de **ReportItem** denominado `Textbox1`:  
  
     `=ReportItems!Textbox1.Value`  
  
-   Esta expresión, ubicada en la propiedad Color de un cuadro de texto de **ReportItem**, muestra el texto en negro cuando el valor es > 0 y en rojo en los demás casos:  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   Esta expresión, ubicada en un cuadro de texto del encabezado o el pie de página, muestra el primer valor de cada página del informe representado, para un cuadro de texto denominado `LastName`:  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>Expresiones de estilo diccionario para los encabezados de página  
 Puede crear un encabezado de página que muestre el primer cliente de la página y el último cliente de la página. Dado que un cuadro de texto del encabezado de página solo puede hacer referencia una vez a la colección integrada **ReportItems** en una expresión, necesita agregar dos cuadros de texto al encabezado de página: uno para el nombre del primer cliente (`=First(ReportItems!textboxLastName.Value`) y otro para el nombre del último cliente (`=Last(ReportItems!textboxLastName.Value`).  
  
 En una sección de encabezado o de pie de página, solo están disponibles los cuadros de texto de la página actual como miembros de la colección **ReportItems** . Por ejemplo, si `ReportItems!textboxLastName.Value` hace referencia a un cuadro de texto que solo aparece en la primera página de una región de datos de varias páginas, verá un valor para la primera página, pero todas las demás páginas mostrarán **#Error** para indicar que la expresión no se pudo evaluar tal como estaba escrita.  
  
## <a name="scope-for-the-reportitems-collection"></a>Ámbito para la colección ReportItems  
 A medida que se procesa el informe, cada cuadro de texto del cuerpo del informe o de una región de datos se evalúa en el contexto de su conjunto de datos, su región de datos y sus asociaciones de grupo. El ámbito para una referencia a la colección **ReportItems** es el ámbito actual o cualquier punto situado más arriba que el ámbito actual.  
  
 Por ejemplo, un cuadro de texto de una fila que está en un grupo primario no debe contener ninguna expresión que haga referencia al nombre de un cuadro de texto de una fila de un grupo secundario. Este tipo de expresión no se resuelve como un valor del informe porque el cuadro de texto de la fila secundaria está fuera del ámbito. Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Ver también  
 [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
