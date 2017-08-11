---
title: "Panel de agrupación (generador de informes) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0f8017dd30a085519f9dd5d3593aaa3d59329f8c
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="grouping-pane-report-builder"></a>Panel de agrupación (Generador de informes)
  El panel de agrupación muestra los grupos de filas y de columnas para la región de datos Tablix seleccionada actualmente. El panel de agrupación no está disponible para las regiones de datos Gráfico o Medidor. El panel de agrupación contiene los paneles Grupos de filas y Grupos de columnas. El panel en cuestión tiene dos modos: predeterminado y avanzado. El modo predeterminado muestra una vista jerárquica de los miembros dinámicos para los grupos de filas y de columnas. El modo avanzado muestra los miembros dinámicos y estáticos para los grupos de filas y de columnas. Un grupo es un conjunto de datos con nombre de un conjunto de datos de informe que se muestra en una región de datos. Los grupos se organizan en jerarquías que incluyen miembros estáticos y dinámicos. Para más información, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Si no ve el panel Agrupación, en la pestaña **Vista**, en el grupo **Mostrar u ocultar**, haga clic en **Agrupación**.  
  
 Las celdas de las áreas de grupos de filas y grupos de columnas pueden ser miembros estáticos o dinámicos de un grupo de filas o de columnas del Tablix. Los miembros estáticos solo se repiten una vez para cada grupo y normalmente contienen etiquetas o totales. Los miembros dinámicos se repiten una vez para cada instancia de grupo y normalmente contienen los valores únicos de la expresión de grupo. A medida que se seleccionan celdas de Tablix en el área de grupos de filas o de grupos de columnas, se selecciona el miembro del grupo correspondiente en el panel Grupos de filas o Grupos de columnas. Y a la inversa, si se seleccionan grupos en el Panel de agrupación, se selecciona en la superficie de diseño la celda correspondiente asociada al miembro de grupo. Para más información sobre las áreas de grupos de filas y columnas de Tablix, vea [Describir las áreas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 El Panel de agrupación admite los modos siguientes:  
  
-   **Predeterminado.** use el modo predeterminado para agregar, modificar o eliminar grupos. Puede agregar grupos primarios, secundarios y de detalles arrastrando campos desde el panel Datos de informe e insertándolos en la jerarquía de grupos. Para agregar un grupo adyacente, debe usar el acceso directo **Agregar grupo** . Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Avanzado**: use el **modo avanzado** para ver todos los miembros de los grupos de filas y de columnas, así como para establecer propiedades en miembros estáticos. Al crear grupos o agregar totales, se establecen automáticamente las propiedades que controlan cómo representa la región de datos Tablix las filas y las columnas en cada página del informe. Para ajustar manualmente estas propiedades, debe establecerlas en el miembro de Tablix. Para más información, vea [Controlar la presentación de la región de datos Tablix en una página de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Modo predeterminado  
 En el modo predeterminado, los paneles Grupos de filas y Grupos de columnas muestran una vista jerárquica para todos los grupos primarios, secundarios y adyacentes. Los grupos secundarios aparecen con una sangría debajo de sus grupos primarios. Los grupos adyacentes aparecen en el mismo nivel de sangría que sus grupos relacionados. La ilustración siguiente muestra una región de datos Tablix con grupos de filas anidados y grupos de columnas anidados y adyacentes.  
  
 ![Tablix, grupos anidados y adyacentes filas y columnas](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, grupos anidados y adyacentes filas y columnas")  
  
 El panel Agrupación muestra los grupos de filas y de columnas correspondientes. En la ilustración siguiente, el grupo basado en subcategorías se ha seleccionado en el panel Grupos de filas, y la celda de agrupamiento [Subcat] está seleccionada en la región de datos Tablix:  
  
 ![Panel de agrupación para los grupos de filas y de columnas anidados](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "panel de agrupación para los grupos anidados de filas y columnas")  
  
 En el panel Grupos de filas, el grupo basado en subcategorías es un grupo secundario del grupo basado en categorías. En el panel Grupos de columnas, el grupo de país/región es un grupo secundario del grupo de geografía. El grupo de años y los grupos de país/región son grupos adyacentes.  
  
 Para más información, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>modo avanzado  
 En el modo avanzado, los paneles Grupos de filas y Grupos de columnas muestran una vista jerárquica para todos los grupos, incluidos los miembros tanto estáticos como dinámicos. Al seleccionar un miembro, el panel Propiedades muestra las propiedades para el miembro de Tablix seleccionado actualmente.  
  
> [!NOTE]  
>  Para activar el **Modo avanzado**, haga clic con el botón derecho en la flecha abajo situada junto al panel Grupos de columnas y, luego, haga clic en **Modo avanzado**.  
  
 En la mayoría de los casos, las propiedades que controlan la presentación de los grupos de columnas y de filas estáticas y dinámicas se establecen automáticamente al crear un grupo o agregar totales. Para modificar los valores predeterminados, debe seleccionar el miembro del grupo en el panel Grupos de filas o Grupos de columnas y, a continuación, cambiar los valores de las propiedades en la ventana Propiedades. Están disponibles las propiedades siguientes:  
  
-   **FixedData**: booleano. Para encabezados de columnas y de filas externas. Inmoviliza el área de grupo de filas al desplazarse verticalmente o el área de grupo de columnas al desplazarse horizontalmente en un representador, como HTML.  
  
-   **HideIfNoRows**: booleano. Solo para miembros estáticos. Si se establece, se omiten Hidden y ToggleItem. Oculte este miembro si la región de datos Tablix no contiene filas de datos.  
  
-   **KeepTogether**: booleano. Indica que todo el miembro de Tablix y cualquiera de los miembros anidados deben mantenerse juntos en una página, si es posible.  
  
-   **KeepWithGroup**: booleano. Solo para miembros de fila estáticos. Siempre que sea posible, mantenga esta fila con el siguiente miembro dinámico relacionado anterior o posterior, si no está oculto. Para mantener un encabezado de fila con su grupo asociado, establezca KeepWithGroup en **After**.  
  
-   **RepeatOnNewPage**: booleano. Solo para miembros de fila estáticos y siempre que KeepWithGroup no sea None. Siempre que sea posible, repita esta fila estática en todas las páginas que tengan al menos una instancia del miembro dinámico especificado por KeepWithGroup. Para mantener un encabezado de fila con su grupo asociado, establezca RepeatOnNewPage en **True**.  
  
-   **Hidden**: booleano. Indica si la fila o la columna debe estar oculta inicialmente.  
  
-   **ToggleItem** : cadena. Nombre del cuadro de texto al que se va a agregar la imagen de alternancia. El cuadro de texto debe estar en el mismo ámbito de grupo o en un ámbito contenedor.  
  
 Para más información, vea [Controlar la presentación de la región de datos Tablix en una página de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md), [Mostrar encabezados y pies de página con un grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md) y [Mostrar encabezados de fila y de columna en varias páginas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 No todos los miembros estáticos tienen un encabezado que corresponde a una celda de la superficie de diseño. En el panel Agrupación, la convención siguiente indica si un miembro estático no tiene ningún encabezado:  
  
-   **Static** : indica un miembro estático con una celda de encabezado.  
  
-   **(Static)** : indica un miembro estático sin celda de encabezado, lo que se denomina miembro estático oculto.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del generador de informes para cuadros de diálogo, paneles y asistentes](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Filtro, grupo y ordenar los datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Tablas, Matrices y listas de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
