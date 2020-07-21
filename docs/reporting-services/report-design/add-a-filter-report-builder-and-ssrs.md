---
title: Adición de un filtro (Generador de informes) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 10ae54e7-0e8a-4dff-995d-05516c51d076
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0eadf07ed347ce2b77eccab229ef6551a62d63d8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080755"
---
# <a name="add-a-filter-report-builder-and-ssrs"></a>Agregar un filtro (Generador de informes y SSRS)
  Agregue un filtro a un conjunto de datos, una región de datos o un grupo cuando desee incluir o excluir valores específicos para la realización de cálculos o la visualización. Los filtros se aplican en tiempo de ejecución y en este orden: primero en el conjunto de datos, a continuación, en la región de datos y, por último, en el grupo; en las jerarquías de grupo, se aplican en orden descendente. En una tabla, matriz o lista, los filtros de los grupos de filas, los grupos de columnas y los grupos adyacentes se aplican de forma independiente. En un gráfico, también se aplican de forma independiente los filtros de los grupos de categorías y los grupos de series.  
  
 Para agregar un filtro, debe especificar una o varias ecuaciones de filtro. Una ecuación de filtro se compone de una expresión que identifica los datos que se van a filtrar, un operador y el valor con el que se va a llevar a cabo la comparación. Los tipos de datos de los datos filtrados y el valor deben coincidir. No está permitido el filtrado por valores agregados para un conjunto de datos o una región de datos.  
  
 Para filtrar los puntos de datos de un gráfico, puede establecer un filtro en un grupo de categorías o en un grupo de series. De manera predeterminada, el gráfico usa la función integrada SUM para agregar valores que pertenecen al mismo grupo en un punto de datos individual de la serie. Si cambia la función de agregado de una serie, deberá cambiar la función de agregado en la expresión de filtro.  
  
 Para más información sobre cómo filtrar conjuntos de datos insertados y compartidos, vea [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-filter-on-a-data-region"></a>Para establecer un filtro en una región de datos  
  
1.  Abra un informe en la vista **Diseño** .  
  
2.  En la superficie de diseño, seleccione la región de datos y, después, haga clic con el botón derecho en _\<Propiedades de_ **<región de datos>** . Si se trata de un medidor, seleccione **Propiedades del panel de medidores**. Se abre el cuadro de diálogo _\<Propiedades de_ **región de datos>** .  
  
    > [!NOTE]  
    >  En una región de datos Tablix, haga clic con el botón derecho en la celda de la esquina o en un identificador de fila o columna y, después, haga clic en **Propiedades de Tablix**.  
  
3.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
4.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
5.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
6.  En la lista desplegable, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
7.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
8.  En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-tablix-row-or-column-group"></a>Para establecer un filtro en un grupo de filas o de columnas de un Tablix  
  
1.  Abra un informe en la vista **Diseño** .  
  
2.  Haga clic con el botón secundario en la tabla, matriz o región de datos de lista de la superficie de diseño para seleccionarla. El panel de agrupación muestra los grupos para el elemento seleccionado.  
  
3.  En el panel de agrupación, haga clic con el botón derecho en el grupo y, después, haga clic en **Editar grupo**. Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
4.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
5.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
6.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
7.  En la lista desplegable, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
8.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
9. En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-category-group"></a>Para establecer un filtro en un grupo de categorías de gráfico  
  
1.  Abra un informe en la vista **Diseño** .  
  
2.  En la superficie de diseño, haga clic dos veces en el gráfico para que aparezcan las zonas de colocación de campos de datos, de serie y de categoría.  
  
3.  Haga clic con el botón derecho en un campo de la zona de colocación de campos de categoría y seleccione **Propiedades del grupo de categorías**.  
  
4.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
5.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
6.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
7.  En la lista desplegable, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
8.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
9. En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-series-group"></a>Para establecer un filtro en un grupo de series de gráfico  
  
1.  Abra un informe en la vista **Diseño** .  
  
2.  En la superficie de diseño, haga clic dos veces en el gráfico para que aparezcan las zonas de colocación de campos de datos, de serie y de categoría.  
  
3.  Haga clic con el botón derecho en un campo de la zona de colocación de campos de serie y seleccione **Propiedades del grupo de series**.  
  
4.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
5.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
6.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
7.  En la lista desplegable, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
8.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
9. En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
