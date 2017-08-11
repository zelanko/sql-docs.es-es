---
title: "Mantener visibles los encabezados al desplazarse a través de un informe (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f2fac57fe0e898a1ccbfbe33fb271eae76da1389
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>Mantener visibles los encabezados al desplazarse a través de un informe (Generador de informes y SSRS)
  Para evitar que las etiquetas de fila y de columna se desplacen fuera de la vista después de representar un informe, puede inmovilizar los encabezados de fila o de columna.  
  
 La forma de controlar las filas y las columnas depende de si tiene una tabla o una matriz. Si tiene una tabla, configure los miembros estáticos (encabezados de fila y columna) para que sigan siendo visibles. Si tiene una matriz, configure los encabezados de grupos de filas y columnas para que sigan siendo visibles.  
  
 Si exporta el informe a Excel, el encabezado no se inmovilizará automáticamente. Puede inmovilizar el panel en Excel. Para obtener más información, consulte el **encabezados de página y pies de página** sección de [exportar a Microsoft Excel &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Aunque una tabla tenga grupos de filas y columnas, no puede mantener esos encabezados de grupo visible durante el desplazamiento  
  
 En la ilustración siguiente se muestra una tabla.  
  
 ![Tabla](../../reporting-services/report-design/media/table.png "tabla")  
  
 En la ilustración siguiente se muestra una matriz.  
  
 ![Matriz](../../reporting-services/report-design/media/matrix.png "matriz")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>Para mantener visibles los encabezados de grupo de matrices al desplazarse  
  
1.  Haga clic con el botón derecho en la fila, columna o controlador de tabla de una región de datos Tablix y, después, haga clic en **Propiedades de Tablix**.  
  
2.  En la pestaña **General** , bajo **Encabezados de fila** o **Encabezados de columna**, seleccione **El encabezado debe permanecer visible durante el desplazamiento**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>Para mantener visible mientras se desplaza un miembro de Tablix estático (fila o columna)  
  
1.  En la superficie de diseño, haga clic en cualquier lugar de la tabla para mostrar los miembros estáticos, así como los grupos, en el panel agrupación.  
  
     ![Panel de agrupación](../../reporting-services/report-design/media/grouppane-updated.png "panel de agrupación")  
  
     El panel Grupos de filas muestra los miembros jerárquicos estáticos y dinámicos de la jerarquía de grupos de fila, mientras que el panel Grupos de columnas muestra una vista similar de la jerarquía de grupos de columna.  
  
2.  En el lado derecho del panel de agrupación, haga clic en la flecha abajo y, a continuación, haga clic en **Modo avanzado**.  
  
3.  Haga clic en el miembro estático (fila o columna) que desea que siga siendo visible durante el desplazamiento. El panel de propiedades muestra las propiedades de **Miembro de Tablix** .  
  
     ![Propiedades de miembro de Tablix](../../reporting-services/report-design/media/grouppane-tablixmember-updated.png "propiedades de miembro de Tablix")  
  
4.  En el panel de propiedades, establezca **FixedData** en **True**.  
  
5.  Repita esto con tantos miembros adyacentes como desee que sean visibles durante el desplazamiento.  
  
6.  Obtenga una vista previa del informe.  
  
 Cuando recorra el informe, los miembros de Tablix estáticos permanecerán visibles.  
  
## <a name="see-also"></a>Vea también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Buscar, ver y administrar informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Mostrar encabezados y pies de página con un grupo de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Mostrar encabezados de fila y columna en varias páginas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [Panel de agrupación &#40; El generador de informes &#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)  
  
  
