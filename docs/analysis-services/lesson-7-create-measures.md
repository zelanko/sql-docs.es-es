---
title: "Lecci&#243;n 7: Crear medidas | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 7: Crear medidas
En esta lección, creará medidas para incluirlas en su modelo. Al igual que las columnas calculadas que creó en la lección anterior, una medida es esencialmente un cálculo creado usando una fórmula DAX. Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro*seleccionado por el usuario; por ejemplo, una columna o una segmentación de datos determinada agregada al campo Etiquetas de filas en una tabla dinámica.   A continuación, la medida aplicada calcula un valor para cada celda del filtro. Las medidas son cálculos eficaces y flexibles que deseará incluir en casi todos los modelos tabulares para realizar cálculos dinámicos sobre datos numéricos. Para obtener más información, vea [Medidas &#40;SSAS tabular&#41;](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Para crear medidas, usará la cuadrícula de medidas. De manera predeterminada, cada tabla tiene una cuadrícula de medidas vacía, pero normalmente no creará medidas para todas las tablas. La cuadrícula de medidas aparece debajo de una tabla en el diseñador de modelos en la vista de datos. Para mostrar u ocultar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y en **Mostrar cuadrícula de medidas**.  
  
Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas y escribiendo después una fórmula DAX en la barra de fórmulas. Al hacer clic en ENTRAR para completar la fórmula, la medida aparecerá en la celda. También puede crear medidas mediante una función de agregación estándar. Para ello, haga clic en una columna y, después, en el botón de autosuma (**∑**) en la barra de herramientas. Las medidas creadas mediante la característica de autosuma aparecerán directamente en la cuadrícula de medidas debajo de la columna, pero se pueden mover si es necesario.  
  
En esta lección, creará medidas escribiendo una fórmula DAX en la barra de fórmulas y usando la característica de autosuma.  
  
Tiempo estimado para completar esta lección: **30 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 6: Crear columnas calculadas](../analysis-services/lesson-6-create-calculated-columns.md).  
  
## Crear medidas  
  
#### Para crear una medida Días del trimestre actual hasta la fecha en la tabla Fecha  
  
1.  En el diseñador de modelos, haga clic en la tabla **Fecha** .  
  
2.  Si no aparece una cuadrícula de medidas vacía debajo de la tabla, haga clic en el menú **Tabla** y después en **Mostrar cuadrícula de medidas**.  
  
3.  En la cuadrícula de medidas, haga clic en la celda vacía superior izquierda.  
  
4.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula:  
  
    **=COUNTROWS( DATESQTD( 'Date'[Fecha]))**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
    Observe que ahora la celda superior izquierda contiene un nombre de medida, **Medida 1**, seguido del resultado, **92**. El nombre de medida también precede a la fórmula en la barra de fórmulas.  
  
5.  Para cambiar el nombre de la medida, en la barra de fórmulas, resalte el nombre, **Medida 1**, escriba **Días del trimestre actual hasta la fecha**y después presione ENTRAR.  
  
    > [!TIP]  
    > Cuando escriba una fórmula en la barra de fórmulas, también puede escribir el nombre de la medida seguido de dos puntos (:) y de la fórmula. Con este método, no tiene que cambiar el nombre de la medida.  
  
#### Para crear una medida Días del trimestre actual en la tabla Fecha  
  
1.  Con la tabla **Fecha** activa en el diseñador de modelos, en la cuadrícula de medidas, haga clic en la celda vacía debajo de la medida que acaba de crear.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    **Días del trimestre actual :=COUNTROWS( DATESBETWEEN( 'Date'[Fecha], STARTOFQUARTER( LASTDATE('Date'[Fecha])), ENDOFQUARTER('Date'[Fecha])))**  
  
    Observe que en esta fórmula primero se incluye el nombre de medida seguido de dos puntos (:).  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
Al crear un coeficiente de comparación entre un período incompleto y el período anterior, la fórmula debe tener en cuenta la parte del período que ha transcurrido y compararla con la misma parte del período anterior. En este caso, [Días del trimestre actual hasta la fecha]/[Días del trimestre actual] da como resultado la parte transcurrida del período actual.  
  
#### Para crear una medida Pedido de venta de recuento distinto por Internet en la tabla Ventas por Internet  
  
1.  En el diseñador de modelos, haga clic en la tabla (pestaña) **Ventas por Internet**.  
  
    Si no aparece la cuadrícula de medidas, haga clic con el botón derecho en la tabla (pestaña) **Venta por Internet** y, después, haga clic en **Mostrar cuadrícula de medidas**.  
  
2.  Haga clic en el encabezado de columna **Número de pedido de venta** .  
  
3.  En la barra de herramientas, haga clic en la flecha abajo situada junto al botón de autosuma (**∑**) y, después, seleccione **DistinctCount**.  
  
    La característica de autosuma crea automáticamente una medida para la columna seleccionada usando la fórmula estándar de agregación DistinctCount.  
  
    Observe que la celda superior situada debajo de la columna en la cuadrícula de medidas ahora contiene un nombre de medida, **Número de pedido de venta de recuento distinto**. Las medidas creadas mediante la característica de autosuma se colocan automáticamente en la celda superior de la cuadrícula de medidas debajo de la columna asociada.  
  
4.  En la cuadrícula de medidas, haga clic en la nueva medida y, a continuación, en la ventana **Propiedades** , en **Nombre de medida**, cambie el nombre de la medida a **Pedido de venta de recuento distinto por Internet**.  
  
#### Para crear medidas adicionales en la tabla Ventas por Internet  
  
1.  Con la característica de autosuma, cree y asigne un nombre a las medidas siguientes:  
  
    |Nombre de medida|Columna|Autosuma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |Recuento de líneas de pedido por Internet|Número de líneas del pedido de venta|Count|=COUNT ([Número de líneas del pedido de venta])|  
    |Unidades totales de Internet|Cantidad del pedido|Sum|=SUM([Cantidad del pedido])|  
    |Importe de descuento total por Internet|Importe de descuento|Sum|=SUM([Importe de descuento])|  
    |Costo total del producto por Internet|Costo total del producto|Sum|=SUM([Costo total del producto])|  
    |Ventas totales por Internet|Importe de ventas|Sum|=SUM([Importe de ventas])|  
    |Margen total por Internet|Margen|Sum|=SUM([Margen])|  
    |Importe de impuesto total por Internet|Importe de impuesto|Sum|=SUM([Importe de impuesto])|  
    |Cargos totales por Internet|Cargos|Sum|=SUM([Cargos])|  
  
2.  Haciendo clic en una celda vacía de la cuadrícula de medidas y usando la barra de fórmulas, cree y asigne un nombre a las medidas siguientes:  
  
    > [!IMPORTANT]  
    > Debe crear las medidas siguientes en orden; las fórmulas de las medidas posteriores hacen referencia a las medidas anteriores.  
  
    |Nombre de medida|Fórmula|  
    |----------------|-----------|  
    |Margen del trimestre anterior por Internet|=CALCULATE ([Margen total por Internet],PREVIOUSQUARTER('Date'[Fecha]))|  
    |Margen del trimestre actual por Internet|=TOTALQTD([Margen total por Internet],'Date'[Fecha])|  
    |Proporción del margen del trimestre anterior por Internet hasta la fecha|=[Margen del trimestre anterior por Internet]*([Días del trimestre actual hasta la fecha]/[Días del trimestre actual])|  
    |Ventas del trimestre anterior por Internet|=CALCULATE([Ventas totales por Internet],PREVIOUSQUARTER('Date'[Fecha]))|  
    |Ventas del trimestre actual por Internet|=TOTALQTD([Ventas totales por Internet],'Date'[Fecha])|  
    |Proporción de ventas del trimestre anterior por Internet hasta la fecha|=[Ventas del trimestre anterior por Internet]*([Días del trimestre actual hasta la fecha]/[Días del trimestre actual])|  
  
Las medidas creadas para la tabla Ventas por Internet se pueden utilizar para analizar datos financieros críticos como ventas, costos y margen de beneficios para los elementos definidos por el filtro seleccionado por el usuario.  
  
## Paso siguiente  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 8: Crear indicadores clave de rendimiento](../analysis-services/lesson-8-create-key-performance-indicators.md).  
  
  
  
