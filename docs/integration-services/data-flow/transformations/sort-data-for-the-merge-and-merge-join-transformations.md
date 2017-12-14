---
title: "Ordenar datos para las transformaciones Mezclar y Combinación de mezcla | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sort attributes [Integration Services]
- output columns [Integration Services]
ms.assetid: 22ce3f5d-8a88-4423-92c2-60a8f82cd4fd
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 75bcc0fbc667921debf0fa27d7cc95103fa4860c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sort-data-for-the-merge-and-merge-join-transformations"></a>Ordenar datos para las transformaciones Mezclar y Combinación de mezcla
  En [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], las transformaciones Mezclar y Combinación de mezcla requieren datos ordenados en sus entradas. Los datos de entrada deben estar ordenados físicamente, y se deben establecer opciones de ordenación en las salidas y en las columnas de salida del origen o en la transformación de nivel superior. Si las opciones de ordenación indican que los datos están ordenados, pero en realidad no lo están, los resultados de la operación de mezcla o combinación de mezcla son impredecibles.  
  
## <a name="sorting-the-data"></a>Ordenar los datos  
 Para ordenar estos datos, puede usar uno de los métodos siguientes:  
  
-   En el origen, use una cláusula ORDER BY en la instrucción empleada para cargar los datos.  
  
-   En el flujo de datos, inserte una transformación Ordenar antes de la transformación Mezclar o Combinación de mezcla.  
  
 Si los datos son cadenas, las transformaciones Mezclar y Combinación de mezcla esperan que los valores de cadena se hayan ordenado usando la intercalación de Windows. Para proporcionar valores de cadena a las transformaciones Mezclar y Combinación de mezcla ordenadas mediante la intercalación de Windows, use el procedimiento siguiente:  
  
#### <a name="to-provide-string-values-that-are-sorted-by-using-windows-collation"></a>Para proporcionar valores de cadena ordenados mediante la intercalación de Windows  
  
-   Utilice una transformación Ordenar para ordenar los datos.  
  
     La transformación Ordenar utiliza la intercalación de Windows para ordenar los valores de cadena.  
  
     O bien  
  
-   Use el operador CAST de Transact-SQL para convertir primero los valores **varchar** en valores **nvarchar** y, después, use la cláusula ORDER BY de Transact-SQL para ordenar los datos.  
  
    > [!IMPORTANT]  
    >  No puede utilizar la cláusula ORDER BY en solitario porque la cláusula ORDER BY utiliza una intercalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para ordenar los valores de cadena. El uso de la intercalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede dar lugar a un criterio de ordenación diferente del obtenido con la intercalación de Windows, lo que puede hacer que la transformación Mezclar o Combinación de mezcla genere resultados inesperados.  
  
## <a name="setting-sort-options-on-the-data"></a>Establecer opciones de ordenación en los datos  
 Hay dos propiedades de ordenación importantes que se deben establecer para el origen o la transformación de nivel superior que proporciona los datos a las transformaciones Mezclar y Combinación de mezcla:  
  
-   La propiedad **IsSorted** de la salida que indica si los datos se han ordenado. Esta propiedad debe estar establecida en **True**.  
  
    > [!IMPORTANT]  
    >  Aunque se establezca el valor de la propiedad **IsSorted** en **True** , los datos no se ordenan. Esta propiedad únicamente proporciona una sugerencia a los componentes de nivel inferior acerca de que los datos se han ordenado previamente.  
  
-   La propiedad **SortKeyPosition** de las columnas de salida que indica si una columna está ordenada, el criterio de ordenación de ésta y la secuencia en la que se ordenan varias columnas. Esta propiedad se debe establecer para cada columna de datos ordenados.  
  
 Si usa una transformación Ordenar para ordenar los datos, esta transformación establece ambas propiedades como requeridas por la transformación Mezclar o Combinación de mezcla. Es decir, la transformación Ordenar establece la propiedad **IsSorted** de su salida en **True**, y establece las propiedades **SortKeyPosition** de sus columnas de resultados.  
  
 Sin embargo, si no usa una transformación Ordenar para ordenar los datos, debe establecer estas propiedades de ordenación manualmente en el origen o en la transformación de nivel superior. Para establecer manualmente las propiedades de ordenación en el origen o en la transformación de nivel superior, use el procedimiento siguiente.  
  
#### <a name="to-manually-set-sort-attributes-on-a-source-or-transformation-component"></a>Para establecer manualmente los atributos de ordenación en un componente de origen o de transformación  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En la pestaña **Flujo de datos** , busque el origen o la transformación de nivel superior adecuados, o arrástrelos desde el **Cuadro de herramientas** hasta la superficie de diseño.  
  
4.  Haga clic con el botón derecho en el componente y haga clic en **Mostrar editor avanzado**.  
  
5.  Haga clic en la pestaña **Propiedades de entrada y salida** .  
  
6.  Haga clic en **Salida de \<nombre del componente>** y establezca la propiedad **IsSorted** en **True**.  
  
    > [!NOTE]  
    >  Si establece manualmente la propiedad **IsSorted** de la salida en **True** y los datos no están ordenados, es posible que falten datos o que haya comparaciones de datos no válidas en la transformación de nivel inferior Mezclar o Combinación de mezcla al ejecutar el paquete.  
  
7.  Expanda **Columnas de salida**.  
  
8.  Haga clic en la columna que desea indicar que esté ordenada y establezca su propiedad **SortKeyPosition** en un valor entero distinto de cero siguiendo estas instrucciones:  
  
    -   El valor entero debe representar una secuencia numérica, a partir de 1 y con incrementos de 1.  
  
    -   Un valor entero positivo indica un criterio de ordenación ascendente.  
  
    -   Un valor entero negativo indica un criterio de ordenación descendente. Si se establece en un número negativo, el valor absoluto del número determina la posición de la columna en la secuencia de ordenación.  
  
    -   El valor predeterminado, 0, indica que la columna no está ordenada. Conserve el valor 0 para las columnas de salida que no forman parte de la ordenación.  
  
     Como ejemplo del modo en que se establece la propiedad **SortKeyPosition** , considere la instrucción Transact-SQL siguiente que carga datos en un origen:  
  
     `SELECT * FROM MyTable ORDER BY ColumnA, ColumnB DESC, ColumnC`  
  
     Para esta instrucción, se establecería la propiedad **SortKeyPosition** para cada columna de la manera siguiente:  
  
    -   Establezca la propiedad **SortKeyPosition** de ColumnA en 1. Esto indica que ColumnA es la primera columna que se va a ordenar y se hará en orden ascendente.  
  
    -   Establezca la propiedad **SortKeyPosition** de ColumnB en -2. Esto indica que ColumnB es la segunda columna que se va a ordenar y se hará en orden descendente.  
  
    -   Establezca la propiedad **SortKeyPosition** de ColumnC en 3. Esto indica que ColumnC es la tercera columna que se va a ordenar y se hará en orden ascendente.  
  
9. Repita el paso 8 para cada columna ordenada.  
  
10. Haga clic en **Aceptar**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Transformación Mezclar](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformación Combinación de mezcla](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarea Flujo de datos](../../../integration-services/control-flow/data-flow-task.md)  
  
  
