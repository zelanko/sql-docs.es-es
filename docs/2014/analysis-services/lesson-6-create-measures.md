---
title: 'Lección 7: crear medidas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef207028ab1b4f6bc084f3f4e515ae37630b771d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078432"
---
# <a name="lesson-7-create-measures"></a>Lección 7: Crear medidas
  En esta lección, creará medidas para incluirlas en su modelo. Al igual que las columnas calculadas que creó en la lección anterior, una medida es esencialmente un cálculo creado usando una fórmula DAX. Pero, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro* seleccionado por el usuario (por ejemplo, una determinada columna o segmentación agregada al campo Etiquetas de fila de una tabla dinámica).   Luego, la medida aplicada calculará un valor para cada celda del filtro. Las medidas son cálculos eficaces y flexibles que deseará incluir en casi todos los modelos tabulares para realizar cálculos dinámicos sobre datos numéricos. Para obtener más información, vea [Medidas &#40;SSAS tabular&#41;](tabular-models/measures-ssas-tabular.md).  
  
 Para crear medidas, usará la cuadrícula de medidas. De forma predeterminada, cada tabla tiene una cuadrícula de medidas vacía, aunque en principio no creará medidas para todas las tablas. La cuadrícula de medidas aparece debajo de una tabla en el diseñador de modelos en la vista de datos. Para mostrar u ocultar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y haga clic en **Mostrar cuadrícula de medidas**.  
  
 Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas y, luego, escribiendo una fórmula DAX en la barra de fórmulas. Al hacer clic en ENTRAR para completar la fórmula, la medida aparecerá en la celda. También puede crear medidas usando una función de agregación estándar; para ello, haga clic en una columna y, luego, haga clic en el botón Autosuma (**∑**) de la barra de herramientas. Las medidas creadas mediante la característica de autosuma aparecerán directamente en la cuadrícula de medidas debajo de la columna, pero se pueden mover si es necesario.  
  
 En esta lección, creará medidas escribiendo una fórmula DAX en la barra de fórmulas y usando la característica de autosuma.  
  
 Tiempo estimado para completar esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 6: Crear columnas calculadas](lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Crear medidas  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>Para crear una medida Días del trimestre actual hasta la fecha en la tabla Fecha  
  
1.  En el diseñador de modelos, haga clic en la tabla **Date** .  
  
2.  Si no aparece una cuadrícula de medidas vacía debajo de la tabla, haga clic en el menú **Tabla** y después en **Mostrar cuadrícula de medidas**.  
  
3.  En la cuadrícula de medidas, haga clic en la celda vacía situada en la esquina superior izquierda.  
  
4.  En la barra de fórmulas, encima de la tabla, escriba la fórmula siguiente:  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
     Observe que ahora la celda superior izquierda contiene un nombre de medida, **Medida 1**, seguido del resultado, **30**. El nombre de medida también precede a la fórmula en la barra de fórmulas.  
  
5.  Para cambiar el nombre de la medida, en la barra de fórmulas, resalte el nombre, `Days Current Quarter to Date` **medida 1**, escriba y, a continuación, presione Entrar.  
  
    > [!TIP]  
    >  Cuando escriba una fórmula en la barra de fórmulas, también puede escribir el nombre de la medida seguido de dos puntos (:), seguido de un espacio y seguido de la fórmula. Con este método, no tiene que cambiar el nombre de la medida.  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>Para crear una medida Días del trimestre actual en la tabla Fecha  
  
1.  Con la tabla **Fecha** activa en el diseñador de modelos, en la cuadrícula de medidas, haga clic en la celda vacía debajo de la medida que acaba de crear.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     Observe que en esta fórmula primero se incluye el nombre de medida seguido de dos puntos (:).  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
 Al crear una relación de comparación entre un período incompleto y el período anterior, la fórmula debe tener en cuenta la parte del período que ha transcurrido y compararla con la misma proporción del período anterior. En este caso, [Días del trimestre actual hasta la fecha]/[Días del trimestre actual] da como resultado la parte transcurrida del período actual.  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>Para crear una medida Pedido de venta de recuento distinto por Internet en la tabla Ventas por Internet  
  
1.  En el diseñador de modelos, haga clic en la tabla (pestaña) **Ventas por Internet** .  
  
     Si no aparece la cuadrícula de medidas, haga clic con el botón derecho en la tabla (pestaña) **Venta por Internet** y, después, haga clic en **Mostrar cuadrícula de medidas**.  
  
2.  Haga clic en el encabezado de columna **Número de pedido de venta** .  
  
3.  En la barra de herramientas, haga clic en la flecha hacia abajo situada junto al botón Autosuma (**∑**) y, luego, seleccione **DistinctCount**.  
  
     La característica Autosuma crea automáticamente una medida para la columna seleccionada con la fórmula de agregación estándar DistinctCount.  
  
     Observe que la celda superior situada debajo de la columna en la cuadrícula de medidas ahora contiene un nombre de medida, **Número de pedido de venta de recuento distinto**. Las medidas creadas mediante la característica de autosuma se colocan automáticamente en la celda superior de la cuadrícula de medidas debajo de la columna asociada.  
  
4.  En la cuadrícula de medidas, haga clic en la nueva medida y, a continuación, en la ventana **Propiedades** , en **Nombre de medida**, cambie el nombre de la medida a **Pedido de venta de recuento distinto por Internet**.  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>Para crear medidas adicionales en la tabla Ventas por Internet  
  
1.  Con la característica Autosuma, cree las siguientes medidas y asígneles un nombre:  
  
    |Nombre de medida|Columna|Autosuma (∑)|Fórmula|  
    |------------------|------------|-------------------|-------------|  
    |Recuento de líneas de pedido por Internet|Número de líneas del pedido de venta|Count|=COUNT ([Número de líneas del pedido de venta])|  
    |Unidades totales de Internet|Cantidad del pedido|Sum|=SUM([Cantidad del pedido])|  
    |Importe de descuento total por Internet|Importe de descuento|Sum|=SUM([Importe de descuento])|  
    |Costo total del producto por Internet|Total Product Cost|Sum|=SUM([Costo total del producto])|  
    |Ventas totales por Internet|Importe de ventas|Sum|=SUM([Importe de ventas])|  
    |Margen total por Internet|Margin|Sum|=SUM([Margin])|  
    |Importe de impuesto total por Internet|Tax Amt|Sum|=SUM([Importe de impuesto])|  
    |Cargos totales por Internet|Freight|Sum|=SUM([Freight])|  
  
2.  Haciendo clic en una celda vacía de la cuadrícula de medidas y usando la barra de fórmulas, cree y asigne un nombre a las medidas siguientes:  
  
    > [!IMPORTANT]  
    >  Debe crear las medidas siguientes en orden; las fórmulas de las medidas posteriores hacen referencia a las medidas anteriores.  
  
    |Nombre de medida|Fórmula|  
    |------------------|-------------|  
    |Margen del trimestre anterior por Internet|=CALCULATE ([Margen total por Internet],PREVIOUSQUARTER('Date'[Fecha]))|  
    |Margen del trimestre actual por Internet|=TOTALQTD([Margen total por Internet],'Date'[Fecha])|  
    |Proporción del margen del trimestre anterior por Internet hasta la fecha|=[Margen del trimestre anterior por Internet]*([Días del trimestre actual hasta la fecha]/[Días del trimestre actual])|  
    |Ventas del trimestre anterior por Internet|=CALCULATE([Ventas totales por Internet],PREVIOUSQUARTER('Date'[Fecha]))|  
    |Ventas del trimestre actual por Internet|=TOTALQTD([Ventas totales por Internet],'Date'[Fecha])|  
    |Proporción de ventas del trimestre anterior por Internet hasta la fecha|=[Ventas del trimestre anterior por Internet]*([Días del trimestre actual hasta la fecha]/[Días del trimestre actual])|  
  
 Las medidas creadas para la tabla Ventas por Internet se pueden utilizar para analizar datos financieros críticos como ventas, costos y margen de beneficios para los elementos definidos por el filtro seleccionado por el usuario.  
  
## <a name="next-step"></a>siguiente paso  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 8: Crear indicadores clave de rendimiento](lesson-7-create-key-performance-indicators.md).  
  
  
