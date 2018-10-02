---
title: Panel de agrupación | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- "10033"
- sql13.rtp.rptdesigner.group.f1
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 8b4bd0b3-ec97-48f8-8bfb-82a53a2f35a1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3609d778973a5813790378c0595b3d51b55be013
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770883"
---
# <a name="grouping-pane"></a>Panel de agrupación
Cuando se diseñan informes de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , el panel de agrupación muestra los grupos de filas y de columnas para la región de datos Tablix seleccionada actualmente. El panel de agrupación no está disponible para las regiones de datos Gráfico o Medidor. El panel Agrupación consta de los paneles Grupos de filas y Grupos de columnas. El panel en cuestión tiene dos modos: predeterminado y avanzado. El modo predeterminado muestra una vista jerárquica de los miembros dinámicos para los grupos de filas y de columnas. El modo avanzado muestra los miembros dinámicos y estáticos para los grupos de filas y de columnas. Un grupo es un conjunto de datos con nombre de un conjunto de datos de informe que se muestra en una región de datos. Los grupos se organizan en jerarquías que incluyen miembros estáticos y dinámicos. Para obtener más información, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Si no ve el panel Agrupación, en el menú **Informe** , haga clic en **Agrupación**.
  
 Las celdas de las áreas de grupos de filas y grupos de columnas pueden ser miembros estáticos o dinámicos de un grupo. Los miembros estáticos solo se repiten una vez para cada grupo y normalmente contienen etiquetas o totales. Los miembros dinámicos se repiten una vez para cada instancia de grupo y normalmente contienen los valores únicos de la expresión de grupo. A medida que se seleccionan celdas de Tablix en el área de grupos de filas o de grupos de columnas, se selecciona el miembro del grupo correspondiente en el panel Grupos de filas o Grupos de columnas. Y a la inversa, si se seleccionan grupos en el Panel de agrupación, se selecciona en la superficie de diseño la celda correspondiente asociada al miembro de grupo. Para más información sobre las áreas de grupos de filas y columnas de Tablix, vea [Describir las áreas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 El Panel de agrupación admite los modos siguientes:  
  
-   **Predeterminado.** use el modo predeterminado para agregar, modificar o eliminar grupos. Puede agregar grupos primarios, secundarios y de detalles arrastrando campos desde el panel Datos de informe e insertándolos en la jerarquía de grupos. Para agregar un grupo adyacente, debe usar el acceso directo **Agregar grupo** . Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Avanzado**: use el **modo avanzado** para ver todos los miembros de los grupos de filas y de columnas, así como para establecer propiedades en miembros estáticos. Al crear grupos o agregar totales, se establecen automáticamente las propiedades que controlan cómo la región de datos Tablix representa las filas y las columnas en cada página del informe. Para ajustar manualmente estas propiedades, debe establecerlas en el miembro del Tablix. Para más información, vea [Controlar la presentación de la región de datos Tablix en una página de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Modo predeterminado  
 En el modo predeterminado, los paneles Grupos de filas y Grupos de columnas muestran una vista jerárquica para todos los grupos primarios, secundarios y adyacentes. Los grupos secundarios aparecen con una sangría debajo de sus grupos primarios. Los grupos adyacentes aparecen en el mismo nivel de sangría que sus grupos relacionados. La ilustración siguiente muestra una región de datos Tablix con grupos de filas anidados y grupos de columnas anidados y adyacentes.  
  
 ![Tablix, grupos de filas y columnas anidadas y adyacentes](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, grupos de filas y columnas anidadas y adyacentes")  
  
 El panel Agrupación muestra los grupos de filas y de columnas correspondientes. En la ilustración siguiente, el grupo basado en subcategorías se ha seleccionado en el panel Grupos de filas, y la celda de agrupamiento [Subcat] está seleccionada en la región de datos Tablix:  
  
 ![Panel de agrupación para grupos de filas y columnas anidadas](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "Panel de agrupación para grupos de filas y columnas anidadas")  
  
 En el panel Grupos de filas, el grupo basado en subcategorías es un grupo secundario del grupo basado en categorías. En el panel Grupos de columnas, el grupo de país/región es un grupo secundario del grupo de geografía. El grupo de años y los grupos de país/región son grupos adyacentes.  
  
 Para más información, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>modo avanzado  
En el modo avanzado, puede ver todos los miembros estáticos y dinámicos de un grupo. Al seleccionar un miembro, la ventana Propiedades muestra las propiedades para el **Miembro de Tablix**seleccionado actualmente.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Para activar el **Modo avanzado**, haga clic con el botón derecho en la flecha abajo situada junto al panel Grupos de columnas y, después, haga clic en **Modo avanzado**.  
  
En la mayoría de los casos, las propiedades que controlan la presentación de los grupos de columnas y de filas estáticas y dinámicas se establecen automáticamente al crear un grupo o agregar totales. 

Para modificar los valores predeterminados, debe seleccionar el miembro del grupo en el panel Grupos de filas o Grupos de columnas y, a continuación, cambiar los valores de las propiedades en la ventana Propiedades. Si el panel de propiedades no está visible, haga clic en **Propiedades** o pulse **F4** en el menú **Ver**.  Están disponibles las propiedades siguientes:  
  
-   **FixedData**: booleano. Para encabezados de columnas y de filas externas. Inmoviliza el área de grupo de filas al desplazarse verticalmente o el área de grupo de columnas al desplazarse horizontalmente en un representador, como HTML.  
  
-   **HideIfNoRows**: booleano. Solo para miembros estáticos. Si se establece, se omiten Hidden y ToggleItem. Oculte este miembro si la región de datos Tablix no contiene filas de datos.  
  
-   **KeepTogether**:  
  
-   **KeepWithGroup**: booleano. Solo para miembros de fila estáticos. Siempre que sea posible, mantenga esta fila con el siguiente miembro dinámico relacionado anterior o posterior, si no está oculto.  
  
-   **RepeatOnNewPage**: booleano. Solo para miembros de fila estáticos y siempre que KeepWithGroup no sea None. Siempre que sea posible, repita esta fila estática en todas las páginas que tengan al menos una instancia del miembro dinámico especificado por KeepWithGroup.  
  
-   **Hidden**: booleano. Indica si la fila o la columna debe estar oculta inicialmente.  
  
-   **ToggleItem** : cadena. Nombre del cuadro de texto al que se va a agregar la imagen de alternancia. El cuadro de texto debe estar en el mismo ámbito de grupo o en un ámbito contenedor.  
  
 Para más información sobre cómo se puede controlar este comportamiento en una región de datos Tablix, vea [Controlar la presentación de la región de datos Tablix en una página de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
 No todos los miembros estáticos tienen un encabezado que corresponde a una celda de la superficie de diseño. En el panel Agrupación, la convención siguiente indica si un miembro estático no tiene ningún encabezado:  
  
-   **Static** : indica un miembro estático con una celda de encabezado.  
  
-   **(Static)** : indica un miembro estático sin celda de encabezado, lo que se denomina miembro estático oculto.  
  
## <a name="see-also"></a>Ver también  
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
