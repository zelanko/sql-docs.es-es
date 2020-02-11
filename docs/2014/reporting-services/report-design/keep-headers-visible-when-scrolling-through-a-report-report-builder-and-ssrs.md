---
title: Mantener visibles los encabezados al desplazarse a través de un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37c3dc20ab537e7cb8bf69099dbd6d24ff384731
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105598"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>Mantener visibles los encabezados al desplazarse a través de un informe (Generador de informes y SSRS)
  Para evitar que las etiquetas de fila y de columna se desplacen fuera de la vista después de representar un informe, puede inmovilizar los encabezados de fila o de columna.  
  
 La forma de controlar las filas y las columnas depende de si tiene una tabla o una matriz. Si tiene una tabla, configure los miembros estáticos (encabezados de fila y columna) para que sigan siendo visibles. Si tiene una matriz, configure los encabezados de grupos de filas y columnas para que sigan siendo visibles.  
  
 Si exporta el informe a Excel, el encabezado no se inmovilizará automáticamente. Puede inmovilizar el panel en Excel. Para más información, vea la sección **Encabezados y pies de página** de [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Aunque una tabla tenga grupos de filas y columnas, no puede mantener esos encabezados de grupo visible durante el desplazamiento  
  
 En la ilustración siguiente se muestra una tabla.  
  
 ![Table](../media/table.png "Tabla")  
  
 En la ilustración siguiente se muestra una matriz.  
  
 ![Matrix](../media/matrix.png "Matrix")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>Para mantener visibles los encabezados de grupo de matrices al desplazarse  
  
1.  Haga clic con el botón derecho en la fila o columna o en el controlador de tabla de una región de datos Tablix y, después, haga clic en **Propiedades de Tablix**.  
  
2.  En la pestaña **General** , bajo **Encabezados de fila** o **Encabezados de columna**, seleccione **El encabezado debe permanecer visible durante el desplazamiento**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>Para mantener visible mientras se desplaza un miembro de Tablix estático (fila o columna)  
  
1.  En la superficie de diseño, haga clic en cualquier lugar de la tabla para mostrar los miembros estáticos, así como los grupos, en el panel agrupación.  
  
     ![Panel de agrupación](../media/grouppane-updated.png "Panel de agrupación")  
  
     El panel Grupos de filas muestra los miembros jerárquicos estáticos y dinámicos de la jerarquía de grupos de fila, mientras que el panel Grupos de columnas muestra una vista similar de la jerarquía de grupos de columna.  
  
2.  En el lado derecho del panel agrupación, haga clic en la flecha hacia abajo y, a continuación, haga clic en **modo avanzado**.  
  
3.  Haga clic en el miembro estático (fila o columna) que desea que siga siendo visible durante el desplazamiento. El panel de propiedades muestra las propiedades de **Miembro de Tablix** .  
  
     ![Propiedades de Miembro de Tablix](../media/grouppane-tablixmember-updated.png "Propiedades de Miembro de Tablix")  
  
4.  En el panel Propiedades, establezca **FixedData** en `True`.  
  
5.  Repita esto con tantos miembros adyacentes como desee que sean visibles durante el desplazamiento.  
  
6.  Obtenga una vista previa del informe.  
  
 Cuando recorra el informe, los miembros de Tablix estáticos permanecerán visibles.  
  
## <a name="see-also"></a>Consulte también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar informes &#40;Generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [Mostrar encabezados y pies de página con un grupo &#40;Generador de informes y SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Mostrar encabezados de fila y de columna en varias páginas &#40;Generador de informes y SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [Panel de agrupación &#40;Generador de informes&#41;](grouping-pane-report-builder.md)  
  
  
