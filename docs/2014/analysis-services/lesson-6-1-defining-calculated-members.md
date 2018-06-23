---
title: Definir miembros calculados | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07f13e1c-0b20-4f9e-ad62-c438983f2785
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: e063de7ce9ea45197c17f4d863c56228d9473e78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202823"
---
# <a name="defining-calculated-members"></a>Definir miembros calculados
  Los miembros calculados son miembros de una dimensión o un grupo de medida que se definen según una combinación de datos del cubo, operadores aritméticos, números y funciones. Por ejemplo, puede crear un miembro calculado que calcule la suma de dos medidas físicas en el cubo. Las definiciones de miembros calculados se almacenan en cubos pero sus valores se calculan en el momento de la consulta.  
  
 Para crear un miembro calculado, utilice el comando **Nuevo miembro calculado** en la pestaña **Cálculos** del Diseñador de cubos. Puede crear un miembro calculado dentro de cualquier dimensión, incluida la dimensión de medidas. También puede colocar un miembro calculado en una carpeta para mostrar en el cuadro de diálogo **Propiedades de cálculo** . Para obtener más información, vea [Cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md), [Cálculos en modelos multidimensionales](multidimensional-models/calculations-in-multidimensional-models.md)y [Crear miembros calculados](multidimensional-models/create-calculated-members.md).  
  
 En las tareas de este tema se definen medidas calculadas para permitir que los usuarios vean el porcentaje de margen de beneficio bruto y el ratio de ventas para ventas por Internet, para ventas del distribuidor y para todas las ventas.  
  
## <a name="defining-calculations-to-aggregate-physical-measures"></a>Definir cálculos para agregar medidas físicas  
  
1.  Abra el Diseñador de cubos para el cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial y, a continuación, haga clic en la pestaña **Cálculos** .  
  
     Observe el comando predeterminado CALCULATE en el panel de las **expresiones de cálculo** y en el panel **Organizador de script** . Este comando especifica que las medidas del cubo deberían agregarse según el valor especificado por sus propiedades AggregateFunction. Los valores de medida normalmente se suman, pero también pueden contarse o agregarse de otra forma.  
  
     La siguiente imagen muestra la pestaña **Cálculos** del Diseñador de cubos.  
  
     ![Pestaña cálculos del Diseñador de cubos](../../2014/tutorials/media/l6-calculatedmembers-1.gif "pestaña cálculos del Diseñador de cubos")  
  
2.  En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Nuevo miembro calculado**.  
  
     En el panel de las **expresiones de cálculo** aparece un nuevo formulario en el que podrá definir las propiedades de este nuevo miembro calculado. El nuevo miembro aparecerá también en el panel **Organizador de script** .  
  
     La siguiente imagen muestra el formulario que aparece en el panel de las **expresiones de cálculo** al hacer clic en **Nuevo miembro calculado**.  
  
     ![Formulario del panel de expresiones de cálculo](../../2014/tutorials/media/l6-calculatedmembers-02.gif "formulario del panel de expresiones de cálculo")  
  
3.  En el **nombre** , cambie el nombre de la medida calculada por `[Total Sales Amount]`.  
  
     Si el nombre de un miembro calculado contiene un espacio, dicho nombre deberá ir entre corchetes.  
  
     Observe que en la lista **Jerarquía primaria** , de manera predeterminada, se crea un nuevo miembro calculado en la dimensión **Measures** . A un miembro calculado de la dimensión Measures también se le denomina con frecuencia medida calculada.  
  
4.  En la pestaña **Metadatos** del panel **Herramientas de cálculo** de la pestaña **Cálculos** , expanda **Medidas** y, a continuación, **Ventas por Internet** para ver los metadatos del grupo de medida **Internet Sales** .  
  
     Puede arrastrar los elementos de metadatos desde el panel **Herramientas de cálculo** al cuadro **Expresión** y agregar entonces operadores y otros elementos para crear expresiones de Expresiones multidimensionales (MDX). O bien, puede escribir la expresión MDX directamente en el cuadro **Expresión** .  
  
    > [!NOTE]  
    >  Si no puede ver los metadatos en el panel **Herramientas de cálculo** , haga clic en **Volver a conectar** en la barra de herramientas. Si esto no funciona, puede que tenga que procesar el cubo o iniciar la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
5.  Arrastre **Internet Sales-Sales Amount** de la pestaña **Metadatos** del panel **Herramientas de cálculo** al cuadro **Expresión** del panel de las **expresiones de cálculo** .  
  
6.  En el **expresión** , escriba un signo más (`+`) después de **[Measures]. [ Importe de ventas de ventas por Internet]**.  
  
7.  En la pestaña **Metadatos** del panel **Herramientas de cálculo** , expanda **Venta del distribuidor**y, después, arrastre **Reseller Sales-Sales Amount** al cuadro **Expresión** del panel de las **expresiones de cálculo** después del signo más (+).  
  
8.  En la lista **Cadena de formato** , seleccione **"Moneda"**.  
  
9. En la lista **Comportamiento si no está vacío** , active las casillas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount**y haga clic en **Aceptar**.  
  
     Las medidas especificadas en la lista **Comportamiento si no está vacío** se usan para resolver consultas NON EMPTY en MDX. Si se especifican una o más medidas en la lista **Comportamiento si no está vacío** , [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tratará al miembro calculado como vacío si todas las medidas especificadas están vacías. Si la propiedad **Non-empty behavior** está en blanco, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] deberá evaluar al miembro calculado para determinar si el miembro está vacío.  
  
     La siguiente imagen muestra el panel de las **expresiones de cálculo** llenado con la configuración especificada en los pasos anteriores.  
  
     ![Panel de expresiones de cálculo de Populated](../../2014/tutorials/media/l6-calculatedmembers-03.gif "panel rellena expresiones de cálculo")  
  
10. En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Vista de script**y revise el script de cálculo en el panel de las **expresiones de cálculo** .  
  
     Observe que el nuevo cálculo se agrega a la expresión CALCULATE inicial; los cálculos individuales se separan con un punto y coma. Observe también que aparece un comentario al principio del script del cálculo. Se recomienda la agregación de comentarios dentro del script de cálculo para grupos de cálculos para ayudarle a usted y a otros programadores a comprender los scripts de cálculo complejos.  
  
11. Agregue una nueva línea al script de cálculo después del comando **Calculate;** y antes del script de cálculo recientemente agregada y, a continuación, agregue el siguiente texto al script en su propia línea:  
  
    ```  
    /* Calculations to aggregate Internet Sales and Reseller Sales measures */  
    ```  
  
     La siguiente imagen muestra los scripts de cálculo tal como deberían aparecer en el panel de las **expresiones de cálculo** en este punto del tutorial.  
  
     ![Las secuencias de comandos en el panel de expresiones de cálculo](../../2014/tutorials/media/l6-calculatedmembers-04.gif "Scripts en el panel de expresiones de cálculo")  
  
12. En la barra de herramientas de la **cálculos** , haga clic en **vista de formulario**, compruebe que `[Total Sales Amount]` está seleccionado en el **organizador de Script** panel y, a continuación, haga clic en  **Nuevo miembro calculado**.  
  
13. Cambiar el nombre de este nuevo miembro calculado por `[Total Product Cost]`y, a continuación, cree la siguiente expresión en el **expresión** cuadro:  
  
    ```  
    [Measures].[Internet Sales-Total Product Cost] + [Measures].[Reseller Sales-Total Product Cost]  
    ```  
  
14. En la lista **Cadena de formato** , seleccione **"Moneda"**.  
  
15. En la lista **Comportamiento si no está vacío** , active las casillas **Internet Sales-Total Product Cost** y **Reseller Sales-Total Product Cost**y haga clic en **Aceptar**.  
  
     Ahora ha definido dos miembros calculados y ambos son visibles en el panel **Organizador de script** . Estos miembros calculados pueden ser utilizados por otros cálculos definidos posteriormente en el script de cálculo. Puede ver la definición de cualquier miembro calculado seleccionando el miembro calculado en el panel **Organizador de script** ; la definición del miembro calculado aparecerá en el panel de las **expresiones de cálculo** de la vista Formulario. Los miembros calculados recientemente definidos no aparecerán en el panel **Herramientas de cálculo** hasta que se hayan implementado estos objetos. Los cálculos no requieren procesamiento.  
  
## <a name="defining-gross-profit-margin-calculations"></a>Definir cálculos de margen de beneficio bruto  
  
1.  Compruebe que `[Total Product Cost]` está seleccionado en el **organizador de Script** panel y, a continuación, haga clic en **nuevo miembro calculado** en la barra de herramientas de la **cálculos** ficha.  
  
2.  En el **nombre** , cambie el nombre de esta nueva medida calculada por `[Internet GPM]`.  
  
3.  En el cuadro **Expresión** , cree la siguiente expresión MDX:  
  
    ```  
    ([Measures].[Internet Sales-Sales Amount] -   
    [Measures].[Internet Sales-Total Product Cost]) /  
    [Measures].[Internet Sales-Sales Amount]  
    ```  
  
4.  En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
5.  En la lista **Comportamiento si no está vacío** , active la casilla **Internet Sales-Sales Amount**y, después, haga clic en **Aceptar**.  
  
6.  En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Nuevo miembro calculado**.  
  
7.  En el **nombre** , cambie el nombre de esta nueva medida calculada por `[Reseller GPM]`.  
  
8.  En el cuadro **Expresión** , cree la siguiente expresión MDX:  
  
    ```  
    ([Measures].[Reseller Sales-Sales Amount] -   
    [Measures].[Reseller Sales-Total Product Cost]) /  
    [Measures].[Reseller Sales-Sales Amount]  
    ```  
  
9. En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
10. En la lista **Comportamiento si no está vacío** , active la casilla **Reseller Sales-Sales Amount**y, después, haga clic en **Aceptar**.  
  
11. En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Nuevo miembro calculado**.  
  
12. En el **nombre** , cambie el nombre de esta medida calculada por `[Total GPM]`.  
  
13. En el cuadro **Expresión** , cree la siguiente expresión MDX:  
  
    ```  
    ([Measures].[Total Sales Amount] -   
    [Measures].[Total Product Cost]) /  
    [Measures].[Total Sales Amount]  
    ```  
  
     Observe que este miembro calculado hace referencia a otros miembros calculados. Como este miembro calculado se calculará después de los miembros calculados a los que hace referencia, se tratará de un miembro calculado válido.  
  
14. En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
15. En la lista **Comportamiento si no está vacío** , active las casillas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount**y haga clic en **Aceptar**.  
  
16. En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Vista de script** y revise los tres cálculos que acaba de agregar al script de cálculo.  
  
17. Agregue una nueva línea al script de cálculo inmediatamente anterior la `[Internet GPM]` cálculo y, a continuación, agregue el siguiente texto al script en su propia línea:  
  
    ```  
    /* Calculations to calculate gross profit margin */  
    ```  
  
     La siguiente imagen muestra el panel **Expresiones** con los tres cálculos nuevos.  
  
     ![Nuevos cálculos en el panel de expresiones de cálculo](../../2014/tutorials/media/l6-calculatedmembers-05.gif "nuevos cálculos en el panel de expresiones de cálculo")  
  
## <a name="defining-the-percent-of-total-calculations"></a>Definir el porcentaje de los cálculos totales  
  
1.  En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Vista de formulario**.  
  
2.  En el **organizador de Script** panel, seleccione `[Total GPM]`y, a continuación, haga clic en **nuevo miembro calculado** en la barra de herramientas de la **cálculos** ficha.  
  
     Si hace clic en el miembro calculado final del panel **Organizador de script** antes de hacer clic en **Nuevo miembro calculado** se asegurará de que el nuevo miembro calculado se escribe al final del script. Los scripts se ejecutan en el orden en el que aparecen en el panel **Organizador de script** .  
  
3.  Cambiar el nombre de este nuevo miembro calculado por `[Internet Sales Ratio to All Products]`.  
  
4.  Escriba la siguiente expresión en el cuadro **Expresión** :  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Internet Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Internet Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Internet Sales-Sales Amount] )  
        End  
    ```  
  
     Esta expresión MDX calcula la contribución al total de ventas por Internet de cada producto. La instrucción Case junto con la función IS EMPTY garantiza que no se produzca un error de división por cero cuando un producto no tiene ventas.  
  
5.  En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
6.  En la lista **Comportamiento si no está vacío** , active la casilla **Internet Sales-Sales Amount**y, después, haga clic en **Aceptar**.  
  
7.  En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Nuevo miembro calculado**.  
  
8.  Cambiar el nombre de este miembro calculado por `[Reseller Sales Ratio to All Products]`.  
  
9. Escriba la siguiente expresión en el cuadro **Expresión** :  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Reseller Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Reseller Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Reseller Sales-Sales Amount] )  
        End  
    ```  
  
10. En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
11. En la lista **Comportamiento si no está vacío** , active la casilla **Reseller Sales-Sales Amount**y, después, haga clic en **Aceptar**.  
  
12. En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Nuevo miembro calculado**.  
  
13. Cambiar el nombre de este miembro calculado por `[Total Sales Ratio to All Products]`.  
  
14. Escriba la siguiente expresión en el cuadro **Expresión** :  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Total Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Total Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Total Sales Amount] )  
        End  
    ```  
  
15. En la lista **Cadena de formato** , seleccione **"Porcentaje"**.  
  
16. En la lista **Comportamiento si no está vacío** , active las casillas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount**y haga clic en **Aceptar**.  
  
17. En la barra de herramientas de la pestaña **Cálculos** , haga clic en **Vista de script**y, a continuación, revise los tres cálculos que acaba de agregar al script de cálculo.  
  
18. Agregue una nueva línea al script de cálculo inmediatamente anterior la `[Internet Sales Ratio to All Products]` cálculo y, a continuación, agregue el siguiente texto al script en su propia línea:  
  
    ```  
    /* Calculations to calculate percentage of product to total product sales */  
    ```  
  
     Ahora ha definido un total de ocho miembros calculados, que están visibles en el panel **Organizador de scripts** cuando se está en la Vista de formulario.  
  
## <a name="browsing-the-new-calculated-members"></a>Examinar los nuevos miembros calculados  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, vaya a la pestaña **Explorador** y, a continuación, haga clic en **Volver a conectar**.  
  
3.  Haga clic en el icono de Excel y, a continuación, haga clic en **Habilitar**.  
  
4.  En el panel **Lista de campos de la tabla dinámica** , expanda la carpeta **Valores** para ver los nuevos miembros calculados de la dimensión Medidas.  
  
5.  Arrastre **Importe de venta total** al área Valores y revise los resultados.  
  
     Arrastre las medidas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount** desde los grupos de medida **Internet Sales** y **Reseller Sales** hasta el área Valores.  
  
     Observe que la medida **Total Sales Amount** es la suma de las medidas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount** .  
  
6.  Agregue la jerarquía definida por el usuario **Categorías de producto** al área de filtro del área **Filtro de informe** y, después, filtre los datos por **Mountain Bikes**.  
  
     Observe que la medida **Total Sales Amount** se calcula para la categoría de ventas del producto **Mountain Bikes** según las medidas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount** de **Mountain Bikes**.  
  
7.  Agregue la jerarquía definida por el usuario **Date.Calendar Date** al área Etiquetas de fila y revise los resultados.  
  
     Observe que la medida **Total Sales Amount** de cada año natural se calcula para la categoría de ventas del producto **Mountain Bikes** según las medidas **Internet Sales-Sales Amount** y **Reseller Sales-Sales Amount** de **Mountain Bikes**.  
  
8.  Agregue las medidas **Total GPM**, **Internet GPM**y **Reseller GPM** al área Valores y, a continuación, revise los resultados.  
  
     Observe que el margen de beneficio bruto para la venta del distribuidor es notablemente inferior al de las ventas a través de Internet, como se muestra en la imagen siguiente.  
  
     ![Panel de datos que muestre las ventas de distribuidor](../../2014/tutorials/media/l6-calculatedmembers-7b.gif "panel de datos que muestre las ventas de distribuidor")  
  
9. Agregue las medidas **Total Sales Ratio to All Products**, **Internet Sales Ratio to All Products**y **Reseller Sales Ratio to All Products** al área Valores.  
  
     Observe que el ratio de las ventas de bicicletas de montaña en relación con todos los productos ha aumentado con el tiempo para las ventas por Internet, pero ha disminuido con el tiempo para la venta del distribuidor. Observe también que el ratio de la venta de bicicletas de montaña con respecto a todos los productos es inferior en la venta por distribuidor que en la venta por Internet.  
  
10. Cambie el filtro de **Mountain Bikes** a **Bikes**, y revise los resultados.  
  
     Observe que el margen de beneficio bruto de todas las bicicletas vendidas a través de distribuidores es negativo, porque las bicicletas de paseo y las bicicletas de carrera se están vendiendo con pérdida.  
  
11. Cambie el filtro a **Accessories**y, a continuación, revise los resultados.  
  
     Observe que la venta de accesorios aumenta con el tiempo pero que estas ventas constituyen solo una pequeña fracción del total de ventas. Observe también que el margen de beneficio bruto para la venta de accesorios es superior que para las bicicletas.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Definir conjuntos con nombre](../analysis-services/lesson-6-2-defining-named-sets.md)  
  
## <a name="see-also"></a>Vea también  
 [Cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Cálculos en modelos multidimensionales](multidimensional-models/calculations-in-multidimensional-models.md)   
 [Crear miembros calculados](multidimensional-models/create-calculated-members.md)  
  
  