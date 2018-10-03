---
title: Agregar o eliminar un grupo en una región de datos (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 989eadf2607854a725855b136ebd58462740aeab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819583"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>Agregar o eliminar un grupo en una región de datos (Generador de informes y SSRS)
En informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , agregue un grupo a una región de datos cuando quiera organizar los datos por un valor o un conjunto de expresiones determinados para presentación y cálculos. Un grupo tiene un nombre y una expresión que identifica qué datos de un conjunto de datos pertenecen al grupo. Para obtener más información sobre los grupos, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
 En una región de datos Tablix, haga clic en la tabla, la matriz o la lista para mostrar el panel Agrupación. Arrastre campos del conjunto de datos al panel Grupo de filas y Grupo de columnas para crear grupos primarios o secundarios. Haga clic con el botón secundario en un grupo existente para agregar un grupo adyacente. Por definición, el grupo de detalles es el grupo más interior y solo se puede agregar como grupo secundario. Haga clic con el botón secundario en un grupo existente para eliminarlo. Las filas y columnas en que se visualizarán los valores del grupo se agregan automáticamente. Para más información, vea [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
 En una región de datos Gráfico, haga clic en el gráfico para mostrar las zonas de colocación. Cree grupos arrastrando campos de conjunto de datos a las zonas de colocación de categorías y de series. Para agregar grupos anidados, agregue varios campos a la zona de colocación.  
  
 De forma predeterminada, no se definen grupos en un medidor. El comportamiento predeterminado para el medidor consiste en agregar todos los valores del campo especificado en un valor que se muestra en el medidor. Para obtener más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>Para agregar un grupo de filas o de columnas primario o secundario a una región de datos Tablix  
  
1.  Arrastre un campo desde el panel **Datos de informe** hasta el panel **Grupos de filas** o el panel **Grupos de columnas** .  
  
    > [!NOTE]  
    >  Si no ve el panel de agrupación, en la pestaña Vista, haga clic en **Agrupación**.  
  
2.  Coloque el campo por encima o por debajo de la jerarquía de grupos usando la barra de guía para situar el grupo como grupo primario o grupo secundario de un grupo existente.  
  
     El grupo se agrega con un nombre, una expresión de grupo y una expresión de ordenación predeterminados que se basan en el nombre del campo.  
  
## <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>Para agregar un grupo de filas o de columnas adyacente a una región de datos Tablix  
  
1.  En el panel Agrupación, haga clic con el botón secundario en un grupo del mismo nivel que el grupo que desea agregar. Haga clic en **Agregar grupo**y, a continuación, en **Adyacente anterior** o en **Adyacente posterior** para especificar dónde se debe agregar el grupo. Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
2.  En **Nombre**, escriba un nombre para el grupo.  
  
3.  En **Expresión de grupo**, escriba una expresión o haga clic en el botón Expresión (**fx**) para crear una expresión.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se agrega un nuevo grupo al panel Agrupación y también se agrega una fila o columna en que mostrar los valores del grupo a la región de datos Tablix de la superficie de diseño.  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Para agregar un grupo de detalles a una región de datos Tablix  
  
1.  En el panel de agrupación, haga clic con el botón derecho en un grupo que sea el grupo secundario más interno, pero no el grupo **Detalles** . Haga clic en **Agregar grupo**y, a continuación, haga clic en **Grupo secundario**. Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
2.  En **Expresión de grupo**, deje en blanco la expresión. Los grupos de detalles no tienen ninguna expresión.  
  
3.  Seleccione **Mostrar datos detallados**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se agrega un nuevo grupo de detalles como un grupo secundario en el panel Agrupación, y el identificador de fila para el grupo seleccionado en el paso 1 muestra el icono de grupo de detalles. Para obtener más información sobre los identificadores, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>Para editar un grupo de filas o de columnas de una región de datos Tablix  
  
1.  En la superficie de diseño del informe, haga clic en cualquier lugar de la región de datos Tablix para seleccionarla. El Panel de agrupación muestra los grupos de filas y de columnas.  
  
2.  Haga clic con el botón derecho en el grupo y, después, haga clic en **Propiedades de grupo**.  
  
3.  En **Nombre**, escriba el nombre del grupo.  
  
4.  En **Expresiones de grupo**, escriba o seleccione una expresión simple, o bien haga clic en el botón Expresión (**fx**) para crear una expresión de grupo.  
  
5.  Haga clic en **Agregar** para crear expresiones adicionales. Todas las expresiones que especifique se combinan utilizando un AND lógico para especificar los datos para este grupo.  
  
6.  (Opcional) Haga clic en **Saltos de página** para establecer las opciones de salto de página.  
  
7.  (Opcional) Haga clic en **Ordenar** para seleccionar o escribir expresiones que especifiquen el criterio de ordenación de los valores del grupo.  
  
8.  (Opcional) Haga clic en **Visibilidad** para seleccionar las opciones de visibilidad del elemento.  
  
9. (Opcional) Haga clic en **Filtros** para establecer filtros para este grupo.  
  
10. (Opcional) Haga clic en **Variables** para definir variables en el ámbito de este grupo a las que se puede tener acceso desde cualquier grupo secundario.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-group-from-a-tablix-data-region"></a>Para eliminar un grupo de una región de datos Tablix  
  
1.  En el panel de agrupación, haga clic con el botón derecho en el grupo y, después, haga clic en **Eliminar grupo**.  
  
2.  En el cuadro de diálogo **Eliminar grupo** , seleccione una de las siguientes opciones:  
  
    -   **Eliminar el grupo y las filas y columnas relacionadas** : elija esta opción para eliminar la definición del grupo y todas las filas relacionadas que muestran datos del grupo. Para el grupo de detalles, si la misma fila pertenece a los datos del grupo y de detalles, solo se eliminan las filas de los datos detallados.  
  
    -   **Eliminar solo el grupo** : elija esta opción para mantener la estructura de la región de datos Tablix y eliminar solo la definición del grupo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>Para eliminar un grupo de detalles de una región de datos Tablix  
  
1.  En el panel de agrupación, haga clic con el botón derecho en el grupo de detalles y, después, haga clic en **Eliminar grupo**.  
  
2.  En el cuadro de diálogo **Eliminar grupo** , seleccione una de las siguientes opciones:  
  
    -   **Eliminar el grupo y las filas y columnas relacionadas** : elija esta opción para eliminar la definición del grupo y todas las filas relacionadas que muestran datos del grupo. Para el grupo de detalles, si la misma fila pertenece a los datos del grupo y de detalles, solo se eliminan las filas de los datos detallados.  
  
    -   **Eliminar solo el grupo** : elija esta opción para mantener la estructura de la región de datos Tablix y eliminar solo la definición del grupo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se elimina el grupo de detalles.  
  
    > [!NOTE]  
    >  Compruebe que, después de quitar una fila de detalles, la expresión de cada celda especifica una expresión de agregado donde corresponda. Si es necesario, edite la expresión para especificar las funciones de agregado que se requieran.  
  
## <a name="see-also"></a>Ver también  
 [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
