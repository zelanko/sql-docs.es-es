---
title: Mostrar los mismos datos en una matriz y en un gráfico (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5ef8b1997685aa776eb93c17d144b6f640ea9d3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209745"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>Mostrar los mismos datos en una matriz y en un gráfico (Generador de informes y SSRS)
  Cuando se desea mostrar los mismos datos en una matriz y en un gráfico, se deben establecer propiedades en ambas regiones de datos para especificar el mismo conjunto de datos, y también las mismas expresiones para los filtros, los grupos, las ordenaciones y los datos.  
  
 Dado que ambas regiones de datos tendrán el mismo antecesor para los datos (el conjunto de datos de informe), puede agregar un botón de ordenación interactiva a la matriz de modo que, cuando se haga clic en él, cambie el criterio de ordenación tanto para la matriz como para el gráfico. Para obtener más información, consulte [agregar una ordenación interactiva a una tabla o matriz &#40;generador de informes y SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Para usar los valores de grupo de columnas de la matriz como una leyenda para el gráfico, debe especificar los colores para los datos de las series en el gráfico y, a continuación, usar los mismos colores como colores de relleno para el fondo de los cuadros de texto en la celda de la matriz que muestra los valores de grupo. Para más información, vea [Especificar colores uniformes en varios gráficos de formas &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 En tiempo de ejecución, su informe puede aparecer desordenado si hay demasiados valores de grupo para sus definiciones de grupo. Es posible que necesite filtrar valores, combinar grupos o ajustar el umbral para que el gráfico combine los grupos automáticamente. Para obtener más información, consulte [vincular varias regiones de datos al mismo conjunto de datos &#40;generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>Para agregar una matriz y un gráfico que muestren los mismos datos  
  
1.  Abra un informe en la vista de diseño.  
  
2.  En la pestaña **Insertar** , en el grupo **Regiones de datos** , haga clic en **Matriz**y, a continuación, haga clic en el cuerpo del informe o en un rectángulo en el cuerpo del informe. Se agregará una matriz al informe.  
  
3.  En la pestaña **Insertar** , en el grupo **Regiones de datos** , haga clic en **Gráfico**y, a continuación, seleccione el tipo de gráfico. Se agregará un gráfico al informe.  
  
4.  (Opcional) En la pestaña **Insertar** , en el grupo **Elementos de informe** , haga clic en **Rectángulo**y, después, haga clic en el informe. Se agregará un rectángulo al informe. Arrastre la matriz y el gráfico de los pasos 2 y 3 hasta el rectángulo.  
  
     Colocando varias regiones de datos en el contenedor de rectángulo, ayudará a controlar cómo se representan la matriz y el gráfico al visualizar el informe.  
  
     En los siguientes pasos, elegirá el campo de conjunto de datos que va a mostrarse tanto en la matriz como en el gráfico.  
  
5.  En el panel Datos de informe, arrastre un campo de conjunto de datos numérico hasta la celda de datos de la matriz.  
  
     De forma predeterminada, se usa la función de agregado Sum para calcular el valor de grupo. Si cambia la función de agregado en la matriz, también debe cambiarla en el gráfico.  
  
6.  En la matriz, haga clic con el botón derecho en la celda con datos, haga clic en **Propiedades de cuadro de texto**y, después, haga clic en **Número**. Elija un formato adecuado para el valor de campo de conjunto de datos.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Arrastre el mismo campo de conjunto de datos que eligió en el paso 3 hasta el área **Valores** del gráfico.  
  
9. En el gráfico, haga clic con el botón derecho en el eje Y, haga clic en **Propiedades del eje**y, después, haga clic en **Número**. Elija el mismo formato para los datos que eligió en el paso 4.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     En los siguientes pasos, establecerá el grupo de filas de la matriz y el grupo de series del gráfico en la misma expresión, así como el criterio de ordenación para el grupo de series del gráfico.  
  
11. En el panel Datos de informe, arrastre el campo de conjunto de datos por el que desea agrupar las filas de la matriz al panel Grupos de filas.  
  
     De forma predeterminada, el grupo de filas de la matriz agrega una expresión de ordenación que es igual que la expresión de grupo.  
  
12. Arrastre el mismo campo de conjunto de datos que usó en el paso 9 al área **Grupos de la serie** del gráfico.  
  
13. Haga clic con el botón derecho en el grupo en el área **Grupos de la serie** y, después, haga clic en **Propiedades del grupo de series**.  
  
14. Haga clic en **Ordenar**.  
  
15. Haga clic en **Agregar**. Aparecerá una nueva fila en la cuadrícula de expresiones de ordenación.  
  
16. En **Ordenar por**, en la lista desplegable, elija el campo de conjunto de datos por el que eligió realizar la agrupación en el paso 9.  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     En los siguientes pasos, establecerá el grupo de columnas de la matriz y el grupo de categorías del gráfico en la misma expresión, así como el criterio de ordenación para el grupo de categorías del gráfico.  
  
18. En el panel Datos de informe, arrastre el campo de conjunto de datos por el que desea agrupar las columnas de la matriz al panel Grupos de columnas.  
  
     De forma predeterminada, el grupo de columnas de la matriz agrega una expresión de ordenación que es igual que la expresión de grupo.  
  
19. Arrastre el mismo campo de conjunto de datos que usó en el paso 16 al área **Grupos de categorías** del gráfico.  
  
20. Haga clic con el botón derecho en el área **Grupos de categorías** y, después, en **Propiedades del grupo de categorías**.  
  
21. Haga clic en **Ordenar**.  
  
22. Haga clic en **Agregar**. Aparecerá una nueva fila en la cuadrícula de expresiones de ordenación.  
  
23. En **Ordenar por**, en la lista desplegable, elija el campo de conjunto de datos por el que eligió realizar la agrupación en el paso 16.  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. Obtenga una vista previa del resultado. Los grupos de filas y de columnas de la matriz muestran los mismos datos que los grupos de series y de categorías del gráfico.  
  
## <a name="see-also"></a>Vea también  
 [Vincular varias regiones de datos al mismo conjunto de datos &#40;Generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Los gráficos &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
