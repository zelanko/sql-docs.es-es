---
title: Agregar una ordenación interactiva a una tabla o una matriz (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10121"
- sql13.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 962f07f5e5f6ce00bc21c362ce905bec2773c28c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893805"
---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>Agregar una ordenación interactiva a una tabla o una matriz (Generador de informes y SSRS)
  Agregue botones de ordenación interactiva para que los usuarios puedan cambiar el criterio de ordenación de las filas y las columnas en las tablas y matrices. Esta característica solo es compatible con los formatos de representación que admiten la interacción con el usuario, como HTML.  
  
 Al crear un botón de ordenación interactiva, debe especificar qué desea ordenar, por qué datos ordenar y el ámbito al que desea aplicar la ordenación. Por ejemplo, puede ordenar las filas de detalles por los apellidos del cliente, los valores de grupo de subcategorías dentro de un grupo de categorías por ventas, o los valores de grupo de categorías y subcategorías combinados por totales.  
  
 Cuando se ve el informe, las columnas que admiten la ordenación interactiva tienen iconos de flecha que cambian para indicar el criterio de ordenación. La primera vez que se hace clic en un botón de ordenación interactiva, los elementos se ordenan de manera ascendente. Los clics sucesivos alternan el criterio de ordenación entre ascendente y descendente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="BackToTop"></a> En este artículo  
 [Ordenar filas de detalles para una tabla sin grupos](#SortingDetailRows)  
  
 [Ordenar un grupo de filas primarias de nivel superior para una tabla o matriz](#SortingTopLevelParent)  
  
 [Ordenar grupos secundarios o filas de detalles para un grupo](#SortingChildGroups)  
  
 [Ordenar filas basadas en una expresión de grupo compleja](#SortingMultipleRowGroups)  
  
 [Sincronizar el criterio de ordenación para varias regiones de datos](#SynchronizingSortOrder)  
  
##  <a name="SortingDetailRows"></a> Ordenar filas de detalles para una tabla sin grupos  
 Agregue un botón de ordenación interactiva a un encabezado de columna para que los usuarios puedan hacer clic en dicho encabezado y ordenar las filas de detalles de una tabla por el valor mostrado en esa columna.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>Para agregar un botón de ordenación interactiva a un encabezado de columna para ordenar la tabla por valor  
  
1.  En la vista de diseño del informe, en una tabla sin grupos, haga clic con el botón derecho en el cuadro de texto del encabezado de columna al que quiere agregar un botón de ordenación interactiva y, luego, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en **Ordenación interactiva**.  
  
3.  Seleccione **Habilitar la ordenación interactiva en este cuadro de texto**.  
  
4.  En **Elija lo que va a ordenar:** , haga clic en **Filas de detalles**.  
  
5.  En **Ordenar por**, especifique una expresión de ordenación. En la lista desplegable, seleccione el campo que corresponda a la columna para la que va a definir una acción de ordenación (por ejemplo, para un encabezado de columna denominado "Title", seleccione `[Title]`). Es preciso especificar una expresión de ordenación.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Repita los pasos del 1 al 6 para cada columna a la que desea agregar un botón de ordenación interactiva.  
  
 Para comprobar la acción de ordenación, haga clic en **Ejecutar** para mostrar una vista previa del informe y, a continuación, haga clic en los botones de ordenación interactiva.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="SortingTopLevelParent"></a> Ordenar un grupo de filas primarias de nivel superior para una tabla o matriz  
 Agregue un botón de ordenación interactiva a un encabezado de columna para que los usuarios puedan hacer clic en dicho encabezado y ordenar las filas del grupo primario de una tabla o matriz por el valor mostrado en esa columna. El orden de los grupos secundarios permanece invariable.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>Para agregar un botón de ordenación interactiva a un encabezado de columna para ordenar los grupos  
  
1.  En una tabla o matriz de una vista de diseño del informe, haga clic con el botón derecho en el cuadro de texto del encabezado de columna para el grupo al que quiere agregar un botón de ordenación interactiva y, luego, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en **Ordenación interactiva**.  
  
3.  Seleccione **Habilitar la ordenación interactiva en este cuadro de texto**.  
  
4.  En **Elija lo que va a ordenar:** , haga clic en **Grupos**.  
  
5.  En la lista desplegable, seleccione el nombre del grupo que va a ordenar. Para los grupos basados en expresiones de grupo simples, el valor **Ordenar por** se rellena con una expresión de grupo.  
  
    > [!NOTE]  
    >  Para las expresiones de grupo complejas, establezca manualmente la expresión **Ordenar por** en el mismo valor que la expresión de grupo.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para comprobar la acción de ordenación, haga clic en **Ejecutar** para mostrar una vista previa del informe y, a continuación, haga clic en los botones de ordenación interactiva.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="SortingChildGroups"></a> Ordenar grupos secundarios o filas de detalles para un grupo  
 Agregue un botón de ordenación interactiva a una fila de encabezado de grupo para que los usuarios puedan ordenar los valores de un grupo secundario perteneciente a un grupo primario u ordenar las filas de detalles para el grupo secundario más interior.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>Para agregar un botón de ordenación interactiva a un cuadro de texto de una fila de encabezado de grupo para ordenar grupos secundarios o filas de detalles  
  
1.  En la vista de diseño del informe, haga clic con el botón derecho en el cuadro de texto de la fila de encabezado de grupo a la que quiere agregar un botón de ordenación interactiva y, luego, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en **Ordenación interactiva**.  
  
3.  Seleccione **Habilitar la ordenación interactiva en este cuadro de texto**.  
  
4.  En **Elija lo que va a ordenar:** , haga clic en una de las siguientes opciones:  
  
    -   **Detalles** : haga clic en **Detalles** para ordenar las filas de detalles. En la lista desplegable, seleccione el campo por el que desea realizar la ordenación. Para esta opción, debe especificar el valor por el que desea ordenar.  
  
    -   **Grupos** : haga clic en **Grupos** para ordenar los valores del grupo secundario. Para esta opción, la expresión **Ordenar por** se rellena automáticamente a partir de la expresión de grupo.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para comprobar la acción de ordenación, haga clic en **Ejecutar** para mostrar una vista previa del informe y, a continuación, haga clic en los botones de ordenación interactiva.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="SortingMultipleRowGroups"></a> Ordenar filas basadas en una expresión de grupo compleja  
 Agregue un botón de ordenación interactiva a un encabezado de columna para que los usuarios puedan hacer clic en dicho encabezado y ordenar los grupos primarios y secundarios combinados. Para lograr este efecto, debe cambiar la expresión de grupo para que sea una expresión compuesta de ambos grupos. Por ejemplo, imagine que una matriz muestra los totales de inventario de una tienda para los artículos agrupados por color y tamaño. Para ordenar las filas basadas en la combinación de color y tamaño, en lugar de tener un grupo para el color y otro para el tamaño, puede definir un grupo basado en la combinación de ambos. Para obtener más información sobre la definición de expresiones de grupo, vea [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 En el procedimiento siguiente, los términos especifican las áreas de la región de datos Tablix. Para obtener más información, vea [Describir las áreas de la región de datos Tablix &#40;Generador de informes y SSRS&#41](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Normalmente, cuando se ordenan filas basadas en varios grupos, se desea ver los totales para las filas ordenadas, sin tener en cuenta los grupos de columnas. En este procedimiento no se usa ningún grupo de columnas. Puede empezar agregando una matriz y quitando el grupo de columnas predeterminado. También podría empezar agregando una tabla y quitando el grupo de detalles.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>Para agregar un botón de ordenación interactiva a un encabezado de columna para ordenar varios grupos  
  
1.  En la vista de diseño del informe, agregue una matriz.  
  
2.  Arrastre un campo numérico hasta la celda de datos para vincular el conjunto de datos a la matriz.  
  
     A continuación, creará un grupo con una expresión de grupo que especifica varios campos y un encabezado de grupo que usará para mostrar los valores de grupo.  
  
3.  Compruebe que la matriz está seleccionada en la superficie de diseño. El panel Agrupación muestra un grupo de filas y otro de columnas de forma predeterminada.  
  
4.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo de filas predeterminado y, luego, haga clic en **Editar grupo**. Se abrirá el cuadro de diálogo **Propiedades de grupo** .  
  
5.  En **Nombre**, reemplace el nombre predeterminado por un nombre que especifique los grupos por los que desea realizar la agrupación.  
  
6.  En **Expresiones de grupo**, en **Agrupar por**, haga clic en el botón Expresión (**fx**) para abrir el cuadro de diálogo **Expresión** .  
  
7.  Escriba la expresión que especifica todos los campos por los que desea agrupar. Por ejemplo, la expresión de grupo siguiente combina un campo denominado Color y un campo denominado Size: `=Fields!Color.Value & Fields!Size.Value`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ahora ha definido el grupo. A continuación, arrastre los campos que desea mostrar al área del cuerpo de Tablix de la matriz. Agregue los campos por los que eligió realizar la agrupación en el paso 7 al área del cuerpo de Tablix, cada uno en su propia columna.  
  
     En este escenario, no es necesaria la primera columna del área de grupos de filas de Tablix. Para eliminar la columna, haga clic con el botón derecho en el encabezado de columna y, luego, haga clic en **Eliminar columnas**. Aparecerá un cuadro de diálogo que le preguntará si desea eliminar los grupos asociados. Haga clic en **No**. El área de grupo de filas se elimina y solo se conserva el área del cuerpo de Tablix.  
  
     A continuación, quitará el grupo de columnas predeterminado.  
  
9. En el panel Grupos de columnas, haga clic con el botón derecho en el grupo de columnas predeterminado y, luego, haga clic en **Eliminar grupo**. Aparecerá un cuadro de diálogo que le preguntará si desea eliminar el grupo y las filas y columnas relacionadas, o solo el grupo. Haga clic en **Eliminar solo el grupo**. Se elimina el grupo de columnas y el área de grupo de columnas. Solo se conserva el área del cuerpo de Tablix.  
  
     A continuación, agregará un botón de ordenación interactiva al cuadro de texto que abarca la matriz.  
  
10. Haga clic en el cuadro de texto de la primera fila y, a continuación, haga clic en **Propiedades de cuadro de texto**.  
  
11. Haga clic en **Ordenación interactiva**.  
  
12. Seleccione **Habilitar la ordenación interactiva en este cuadro de texto**.  
  
13. En **Elija lo que va a ordenar:** , haga clic en **Grupos**.  
  
14. En la lista desplegable, seleccione el nombre del grupo que creó en el paso 5. La expresión de grupo se copia automáticamente en el cuadro de texto **Ordenar por** .  
  
15. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ha agregado el botón de ordenación al cuadro de texto.  
  
16. (Opcional) Puede suprimir los valores duplicados en las columnas que muestran valores de grupo. En la superficie de diseño del informe, haga clic en el cuadro de texto que muestra el valor para el que desea ocultar los valores repetidos. En el panel Propiedades, desplácese a **HideDuplicates**y, en la lista desplegable, seleccione el nombre del conjunto de datos que está vinculado a esta matriz.  
  
 Para comprobar la acción de ordenación, haga clic en **Ejecutar** para mostrar una vista previa del informe y, a continuación, haga clic en el botón de ordenación interactiva. La matriz realiza la ordenación por los valores combinados de la expresión de grupo, aunque cada valor individual se muestra en su propia columna.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="SynchronizingSortOrder"></a> Sincronizar el criterio de ordenación para varias regiones de datos  
 Agregue un botón de ordenación interactiva que permita a los usuarios hacer clic en un botón de ordenación y ordenar varias regiones de datos. Al crear un botón de ordenación interactiva, puede especificar si desea sincronizar la ordenación para varias regiones de datos basadas en el mismo conjunto de datos de informe. Por ejemplo, un informe podría incluir una matriz y un gráfico que represente gráficamente los datos. Cuando un usuario cambia el criterio de ordenación de las filas de la matriz, el gráfico muestra automáticamente el mismo criterio de ordenación.  
  
 Para sincronizar el criterio de ordenación, debe usar expresiones de ordenación idénticas para las regiones de datos o grupos que desea ordenar, así como definir el ámbito de la ordenación de tal forma que sea un antecesor mutuo de ambas regiones de datos. El antecesor mutuo puede ser el conjunto de datos al que están vinculadas ambas regiones de datos o una región de datos contenedora dentro de la que aparecen ambas regiones de datos. Por ejemplo, imagine que un informe tiene una matriz y un gráfico que muestran datos del mismo conjunto de datos y que están incluidos en una lista. Para sincronizar la acción de ordenación, debe especificar la ordenación interactiva en una columna de la matriz y establecer el ámbito en la lista. Cuando el usuario ordena la matriz, el gráfico también se ordena.  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>Para sincronizar el criterio de ordenación con un gráfico para un botón de ordenación interactiva en una región de datos de matriz  
  
1.  En la vista de diseño del informe, agregue una matriz al informe.  
  
2.  Agregue un campo de conjunto de datos numérico a la celda de datos de la matriz; por ejemplo, un campo que represente una cantidad o cifras de ventas.  
  
3.  Defina un grupo de filas. De forma predeterminada, el criterio de ordenación para el grupo se establece en la misma expresión que la expresión de grupo.  
  
4.  Agregue un gráfico al informe; por ejemplo, un gráfico circular.  
  
5.  Arrastre el campo que eligió en el paso 2 al área **Valor** del panel **Datos del gráfico** .  
  
6.  Arrastre el campo por el que decidió realizar la agrupación al área **Grupos de Categorías** .  
  
     La expresión de grupo para el grupo de filas de matriz y el grupo de categorías de gráfico debe ser idéntica.  
  
7.  Haga clic con el botón derecho en el grupo de categorías y, luego, haga clic en **Propiedades del grupo de categorías**.  
  
8.  Haga clic en **Ordenar**.  
  
9. Haga clic en **Agregar**. Se agrega una nueva fila de ordenación a la cuadrícula de opciones de ordenación.  
  
10. En Ordenar por, en la lista desplegable, elija el mismo campo que eligió en el paso 6 para realizar la agrupación.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
12. En la matriz, haga clic con el botón derecho en el cuadro de texto en el encabezado de columna al que quiere agregar un botón de ordenación interactiva y, luego, haga clic en **Propiedades de cuadro de texto**.  
  
13. Haga clic en **Ordenación interactiva**.  
  
14. Seleccione **Habilitar la ordenación interactiva en este cuadro de texto**.  
  
15. En **Elija lo que va a ordenar:** , haga clic en **Grupos**.  
  
16. En la lista desplegable de **Grupos**, seleccione el nombre del grupo que va a ordenar. La expresión de grupo para este grupo se establece automáticamente para el valor **Ordenar por** .  
  
17. Seleccione **Aplicar también esta ordenación a otros grupos y regiones de datos de**. En el cuadro de texto, escriba el nombre del conjunto de datos; por ejemplo, "SalesData".  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para comprobar la acción de ordenación, haga clic en **Ejecutar** para mostrar una vista previa del informe y, a continuación, haga clic en el botón de ordenación interactiva. La matriz realiza la ordenación por los valores combinados de la expresión de grupo, aunque cada valor individual se muestra en su propia columna.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ordenación interactiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)   
 [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Explorar la flexibilidad de una región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
