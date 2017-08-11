---
title: "Establecer un mensaje no hay datos para una región de datos (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6d349eece0774513a2552fa1f7248ca89165769
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>Establecer un mensaje para cuando no hay datos en una región de datos (Generador de informes y SSRS)
  Cuando quiera especificar el texto que se debe mostrar en el informe representado en lugar de una región de datos que no tiene datos, establezca la propiedad NoRowsMessage para una región de datos de tabla, matriz o lista, la propiedad NoDataMessage para una región de datos de gráfico y la propiedad NoDataText para la escala de colores de un mapa. En tiempo de ejecución, el procesador de informes ejecuta la consulta para cada conjunto de datos de un informe y la consulta del conjunto de datos puede no generar ningún conjunto de resultados. En las regiones de datos enlazadas a conjuntos de datos vacíos, es posible especificar el texto que se debe mostrar en lugar de mostrar una región de datos vacía. También se puede establecer la propiedad NoRowsMessage para un subinforme cuando ningún conjunto de datos de dicho subinforme tenga datos en tiempo de ejecución.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>Para establecer la propiedad NoRowsMessage para una tabla, una matriz o una lista  
  
1.  En la vista Diseño, haga clic en la región de datos de tabla, matriz o lista o en el subinforme en la superficie de diseño para seleccionarlo. Las propiedades del elemento seleccionado aparecen en el panel de propiedades.  
  
2.  En el panel de propiedades, escriba el texto que desea mostrar como mensaje en el campo de la propiedad **NoRowsMessage** .  
  
     Como alternativa, en la lista desplegable, haga clic en **Expresión** para abrir el cuadro de diálogo **Expresión** y crear una expresión.  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>Para establecer la propiedad NoDataMessage para un gráfico  
  
1.  En la vista Diseño, haga clic en el gráfico en la superficie de diseño para seleccionarlo. Las propiedades del elemento seleccionado aparecen en el panel de propiedades.  
  
2.  En el panel de propiedades, expanda el nodo para **NoDataMessage**.  
  
3.  En **Título**, escriba el texto que desea que se muestre como mensaje en el campo de propiedades **NoDataMessage** .  
  
     Como alternativa, en la lista desplegable, haga clic en **Expresión** para abrir el cuadro de diálogo **Expresión** y crear una expresión.  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>Para establecer la propiedad NoRowsMessage para un subinforme  
  
1.  En la vista Diseño, haga clic en el subinforme en la superficie de diseño para seleccionarlo. Las propiedades del elemento seleccionado aparecen en el panel de propiedades.  
  
2.  En el panel de propiedades, escriba el texto que desea mostrar como mensaje en el campo de la propiedad **NoRowsMessage** .  
  
     Como alternativa, en la lista desplegable, haga clic en **Expresión** para abrir el cuadro de diálogo **Expresión** y crear una expresión.  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>Para establecer la propiedad NoDataText para la escala de colores de un mapa  
  
1.  En la vista Diseño, haga clic en la escala de colores del mapa para seleccionarla. Las propiedades del elemento seleccionado aparecen en el panel de propiedades.  
  
2.  En el panel Propiedades, en **NoDataText**, escriba el texto que desea mostrar como etiqueta para los colores que no tengan valores de datos.  
  
     Como alternativa, en la lista desplegable, haga clic en **Expresión** para abrir el cuadro de diálogo **Expresión** y crear una expresión.  
  
## <a name="see-also"></a>Vea también  
 [Subinformes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [Tablas, Matrices y listas de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Mapas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Subinformes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)  
  
  
