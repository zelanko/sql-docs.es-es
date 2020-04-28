---
title: Definir y examinar KPI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 648b9a02-1278-4f11-b940-6f0de6a4042d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f8a95c5819d88013a0e4f0e0be0aa21c11c1949
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175254"
---
# <a name="defining-and-browsing-kpis"></a>Definir y examinar KPI
  Para definir indicadores clave de rendimiento (KPI), deberá primero definir un nombre de KPI y el grupo de medida con el que desea asociar el KPI. Un KPI se puede asociar con todos los grupos de medida o con un solo grupo de medida. Se definirán entonces los siguientes elementos del KPI:

-   La expresión de valor

     Una expresión de valor es una medida física como Sales, una medida calculada como Profit o un cálculo que se define dentro del KPI mediante una expresión de Expresiones Multidimensionales (MDX).

-   La expresión objetivo

     Una expresión objetivo es un valor, o una expresión MDX que se resuelve en un valor, que define el objetivo de la medida definida por la expresión de valor. Por ejemplo, una expresión objetivo podría ser la cantidad en la que los responsables de una compañía desean incrementar las ventas o el beneficio.

-   La expresión de estado

     Una expresión de estado es una expresión MDX que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza para evaluar el estado actual de la expresión de valor en comparación con la expresión objetivo. Una expresión objetivo es un valor normalizado en el intervalo de -1 a +1, donde -1 es muy malo y +1 es muy bueno. La expresión de estado muestra un gráfico para ayudarle a determinar fácilmente el estado de la expresión de valor en comparación con la expresión objetivo.

-   La expresión de tendencia

     Una expresión de tendencia es una expresión MDX que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza para evaluar la tendencia actual de la expresión de valor en comparación con la expresión objetivo. La expresión de tendencia ayuda al usuario corporativo a determinar rápidamente si la expresión de valor está mejorando o empeorando en relación con la expresión objetivo. Puede asociar uno de los diversos gráficos con la expresión de tendencia para ayudar a los usuarios corporativos a comprender rápidamente la tendencia.

 Además de estos elementos definidos para un KPI, también deben definirse varias propiedades de un KPI. Estas propiedades incluyen una carpeta de muestra, un KPI primario si el KPI se calcula desde otros KPI, el miembro de hora actual si lo hay, el peso del KPI si lo tiene y una descripción del KPI.

> [!NOTE]
>  Para obtener más ejemplos de KPI, consulte los ejemplos de KPI en la pestaña Plantillas del panel Herramientas de cálculo o en los ejemplos del almacenamiento de datos de ejemplo **Adventure Works DW 2012** . Para obtener más información sobre cómo instalar esta base de datos, consulte [Instalar los datos y proyectos de ejemplo para el tutorial de modelado multidimensional de Analysis Services](install-sample-data-and-projects.md).

 En las tareas de esta lección definirá los KPI del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, examinará el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con estos KPI. Definirá los siguientes KPI:

-   Reseller Revenue

     Este KPI se utiliza para medir la forma en que comparar las ventas reales del distribuidor con las cuotas de venta para ventas del distribuidor, la distancia que separa las ventas del el objetivo y qué tendencia se dirige al objetivo.

-   Product Gross Profit Margin

     Este KPI se utiliza para determinar la distancia que existe entre el margen de beneficio bruto de cada categoría de producto y el objetivo especificado de cada categoría de producto, y también para determinar la tendencia hasta alcanzar este objetivo.

## <a name="defining-the-reseller-revenue-kpi"></a>Definir el KPI Reseller Revenue

1.  Abra el Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, después, haga clic en la pestaña **KPI** .

     La pestaña **KPI** incluye varios paneles. En la parte izquierda de la pestaña están el panel **Organizador de KPI** y el panel **Herramientas de cálculo** . El panel de información del centro de la pestaña contiene los detalles del KPI seleccionado en el panel **Organizador de KPI** .

     La siguiente imagen muestra la pestaña **KPI** del Diseñador de cubos.

     ![Pestaña KPIs del Diseñador de cubos](../../2014/tutorials/media/l7-kpi-1.gif "Pestaña KPIs del Diseñador de cubos")

2.  En la barra de herramientas de la pestaña **KPI** , haga clic en el botón **Nuevo KPI** .

     En el panel de información aparecerá una plantilla de KPI en blanco, como en la siguiente imagen.

     ![Plantilla KPI en blanco en el panel de información](../../2014/tutorials/media/l7-kpi-2.gif "Plantilla KPI en blanco en el panel de información")

3.  En el cuadro **nombre** , escriba `Reseller Revenue`y, a continuación, seleccione **reseller sales** en la lista **grupo de medida asociado** .

4.  En la pestaña **Metadatos** del panel **Herramientas de cálculo** , expanda **Medidas**, **Reseller Sales**y, después, arrastre la medida **Reseller Sales-Sales Amount** al cuadro **Expresión de valor** .

5.  En la pestaña **Metadatos** del panel **Herramientas de cálculo** , expanda **Medidas**, **Sales Quotas**y,después, arrastre la medida **Sales Amount Quota** al cuadro **Expresión objetivo** .

6.  Compruebe que está seleccionado **Indicador** en la lista **Indicador de estado** y, después, escriba la siguiente expresión MDX en el cuadro **Expresión de estado** :

    ```
    Case
     When 
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.95
       Then 1
     When
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")<.95
       And 
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.85
       Then 0
      Else-1
    End
    ```

     Esta expresión MDX proporciona lo básico para evaluar el progreso hacia el objetivo. En esta expresión MDX, si las ventas reales del distribuidor están por encima del 85 por ciento del objetivo, se utilizará un valor de 0 para llenar el gráfico seleccionado. Como el gráfico seleccionado es un indicador, el puntero del indicador estará a mitad de camino entre el estado vacío y el lleno. Si las ventas reales por distribuidor están por encima del 90 por ciento, el puntero del indicador ocupará tres cuartas partes del espacio entre vacío y lleno.

7.  Compruebe que está seleccionado **Flecha estándar** en la lista **Indicador de tendencia** y, después, escriba la siguiente expresión en el cuadro **Expresión de tendencia** :

    ```
    Case
     When IsEmpty
      (ParallelPeriod
       ([Date].[Calendar Date].[Calendar Year],1,
           [Date].[Calendar Date].CurrentMember))
      Then 0  
     When  (
      KpiValue("Reseller Revenue") - 
       (KpiValue("Reseller Revenue"), 
        ParallelPeriod
         ([Date].[Calendar Date].[Calendar Year],1,
           [Date].[Calendar Date].CurrentMember))
          /
          (KpiValue ("Reseller Revenue"),
           ParallelPeriod
            ([Date].[Calendar Date].[Calendar Year],1,
             [Date].[Calendar Date].CurrentMember)))
           >=.02
      Then 1
       When(
        KpiValue("Reseller Revenue") - 
         (KpiValue ( "Reseller Revenue" ),
          ParallelPeriod
           ([Date].[Calendar Date].[Calendar Year],1,
            [Date].[Calendar Date].CurrentMember))
           /
            (KpiValue("Reseller Revenue"),
             ParallelPeriod
              ([Date].[Calendar Date].[Calendar Year],1,
                [Date].[Calendar Date].CurrentMember)))
            <=.02
      Then -1
       Else 0
    End
    ```

     Esta expresión MDX proporciona lo básico para evaluar la tendencia hasta lograr el objetivo definido.

## <a name="browsing-the-cube-by-using-the-reseller-revenue-kpi"></a>Examinar el cubo mediante el KPI Reseller Revenue

1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.

2.  Cuando la implementación se haya completado correctamente, haga clic en el botón **Vista de explorador** de la barra de herramientas de la pestaña **KPI** y, después, haga clic en **Volver a conectar**.

     Los indicadores de estado y de tendencia aparecen en el panel **Examinador de KPI** para ventas por distribuidor basadas en valores para el miembro predeterminado de cada dimensión, junto con el valor para el valor y el objetivo. El miembro predeterminado de cada dimensión es el miembro Todos del nivel Todos, porque no ha definido ningún otro miembro de ninguna otra dimensión como miembro predeterminado.

3.  En el panel de filtros, seleccione **Sales Territory** en la lista **Dimensión** , seleccione **Sales Territories** en la lista **Jerarquía** , seleccione **Igual** en la lista **Operador** , active la casilla **Norteamérica** en la lista **Expresión de filtro** y, después, haga clic en **Aceptar**.

4.  En la fila siguiente del panel **Filtro** , seleccione **Date** en la lista **Dimensión** , seleccione **Calendar Date** en la lista **Jerarquía** , seleccione **Igual** en la lista **Operador** , active la casilla **Q3 CY 2007** en la lista **Expresión de filtro** y, después, haga clic en **Aceptar**.

5.  Haga clic en cualquier sitio del panel **Explorador de KPI** para actualizar los valores para el KPI **Reseller Revenue KPI**.

     Observe que las secciones **Valor**, **Objetivo**y **Estado** del KPI reflejan los valores para el nuevo período de tiempo

## <a name="defining-the-product-gross-profit-margin-kpi"></a>Definir el KPI Product Gross Profit Margin

1.  Haga clic en el botón **Vista de formulario** de la barra de herramientas de la pestaña **KPI** y, después, haga clic en el botón **Nuevo KPI** .

2.  En el cuadro **nombre** , escriba `Product Gross Profit Margin`y, a continuación, compruebe que ** \<todos los>** aparecen en la lista **grupo de medida asociado** .

3.  En la pestaña **Metadatos** del panel **Herramientas de cálculo** , arrastre la medida **Total GPM** al cuadro **Expresión de valor** .

4.  En el cuadro **Expresión objetivo** , escriba la expresión siguiente:

    ```
    Case
        When [Product].[Category].CurrentMember Is
          [Product].[Category].[Accessories]
        Then .40                 
        When [Product].[Category].CurrentMember 
          Is [Product].[Category].[Bikes]
        Then .12                
        When [Product].[Category].CurrentMember Is
          [Product].[Category].[Clothing]
        Then .20
        When [Product].[Category].CurrentMember Is
          [Product].[Category].[Components]
        Then .10
        Else .12            
    End
    ```

5.  En la lista **Indicador de estado** , seleccione **Cilindro**.

6.  Escriba la siguiente expresión MDX en el cuadro **Expresión de estado** :

    ```
    Case
        When KpiValue( "Product Gross Profit Margin" ) / 
             KpiGoal ( "Product Gross Profit Margin" ) >= .90
        Then 1
        When KpiValue( "Product Gross Profit Margin" ) / 
             KpiGoal ( "Product Gross Profit Margin" ) <  .90
             And 
             KpiValue( "Product Gross Profit Margin" ) / 
             KpiGoal ( "Product Gross Profit Margin" ) >= .80
        Then 0
        Else -1
    End
    ```

     Esta expresión MDX proporciona lo básico para evaluar el progreso hacia el objetivo.

7.  Compruebe que está seleccionado **Flecha estándar** en la lista **Indicador de tendencia** y, después, escriba la siguiente expresión MDX en el cuadro **Expresión de tendencia** :

    ```
    Case
    When IsEmpty
      (ParallelPeriod
       ([Date].[Calendar Date].[Calendar Year],1,
           [Date].[Calendar Date].CurrentMember))
      Then 0  
       When VBA!Abs
        (
          KpiValue( "Product Gross Profit Margin" ) - 
           (
             KpiValue ( "Product Gross Profit Margin" ),
              ParallelPeriod
              ( 
                [Date].[ Calendar Date].[ Calendar Year],
                1,
                [Date].[ Calendar Date].CurrentMember
              )
            ) /
            (
              KpiValue ( "Product Gross Profit Margin" ),
              ParallelPeriod
              ( 
                [Date].[ Calendar Date].[ Calendar Year],
                1,
                [Date].[ Calendar Date].CurrentMember
              )
            )  
          ) <=.02
      Then 0
      When KpiValue( "Product Gross Profit Margin" ) - 
           (
             KpiValue ( "Product Gross Profit Margin" ),
             ParallelPeriod
             ( 
               [Date].[ Calendar Date].[ Calendar Year],
               1,
               [Date].[ Calendar Date].CurrentMember
             )
           ) /
           (
             KpiValue ( "Product Gross Profit Margin" ),
             ParallelPeriod
             ( 
               [Date].[Calendar Date].[Calendar Year],
               1,
               [Date].[Calendar Date].CurrentMember
             )
           )  >.02
      Then 1
      Else -1
    End
    ```

     Esta expresión MDX proporciona lo básico para evaluar la tendencia hasta lograr el objetivo definido.

## <a name="browsing-the-cube-by-using-the-total-gross-profit-margin-kpi"></a>Examinar el cubo mediante el KPI Total Gross Profit Margin

1.  En el menú **Generar** , haga clic en **Implementar Tutorial de Analysis Services**.

2.  Cuando la implementación se haya completado correctamente, haga clic en **Volver a conectar** en la barra de herramientas de la pestaña **KPI** y, después, haga clic en **Vista de explorador**.

     Aparece `Product Gross Profit Margin` el KPI y muestra el valor de KPI del **tercer trimestre 2007** y el **Norteamérica** territorio de ventas.

3.  En el panel **Filtro** , seleccione **Product** en la lista **Dimensión** , seleccione **Category** en la lista **Jerarquía** , seleccione **Igual** en la lista **Operador** y **Bikes** en la lista **Expresión de filtro** y, después, haga clic en **Aceptar**.

     Aparecerá el margen de beneficio bruto para la venta de bicicletas por distribuidor en Norteamérica en el tercer trimestre de 2007.

## <a name="next-lesson"></a>Lección siguiente
 [Lección 8: definir acciones](lesson-8-defining-actions.md)


