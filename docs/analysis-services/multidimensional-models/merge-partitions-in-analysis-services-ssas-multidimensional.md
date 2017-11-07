---
title: Mezclar particiones en Analysis Services (SSAS - Multidimensional) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], merging
- merging partitions [Analysis Services]
ms.assetid: b3857b9b-de43-4911-989d-d14da0196f89
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a973f81fbb9eef7294b9beec9251569bcce0bf4f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="merge-partitions-in-analysis-services-ssas---multidimensional"></a>Mezclar particiones en Analysis Services (SSAS - Multidimensional)
  Puede mezclar particiones de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente para consolidar datos de hechos de varias particiones del mismo grupo de medida.  
  
 [Escenarios frecuentes](#bkmk_Scenario)  
  
 [Requisitos](#bkmk_prereq)  
  
 [Actualizar el origen de la partición después de mezclar particiones](#bkmk_Where)  
  
 [Consideraciones especiales para las particiones segmentadas por una tabla de hechos o por una consulta con nombre](#bkmk_fact)  
  
 [Cómo mezclar particiones mediante SSMS](#bkmk_partitionSSMS)  
  
 [Cómo mezclar particiones mediante XMLA](#bkmk_partitionsXMLA)  
  
##  <a name="bkmk_Scenario"></a> Escenarios frecuentes  
 La configuración única más común para el uso de particiones entraña la separación de datos a lo largo de la dimensión temporal. La granularidad del tiempo asociada con cada partición varía dependiendo de los requisitos empresariales específicos del proyecto. Por ejemplo, la segmentación puede ser por años, estando el año más reciente dividido por meses, más una partición independiente para el mes activo. La partición del mes activo recibe periódicamente nuevos datos.  
  
 Cuando el mes activo esté completo, dicha partición se volverá a mezclar con los meses de la partición anual y el proceso continuará. Al final del año, se habrá formado toda una partición anual nueva.  
  
 Como muestra este escenario, la mezcla de particiones puede convertirse en una tarea rutinaria que se realiza periódicamente, proporcionando un método progresivo para consolidar y organizar los datos históricos.  
  
##  <a name="bkmk_prereq"></a> Requisitos  
 Solo puede mezclar particiones si todas ellas cumplen los siguientes criterios:  
  
-   Tienen el mismo grupo de medida.  
  
-   Tienen la misma estructura.  
  
-   Deben estar en un estado procesado.  
  
-   Tienen los mismos modos de almacenamiento.  
  
-   Contienen diseños de agregaciones idénticos.  
  
-   Comparten el mismo nivel de compatibilidad de almacén de cadenas (solo se aplica a los grupos de medidas de recuento diferentes con particiones).  
  
 Si la partición de destino está vacía (es decir, tiene un diseño de agregaciones pero ninguna agregación), la mezcla quitará las agregaciones para las particiones de origen. Debe ejecutar Procesar índice, Procesar completo o Procesar predeterminado en la partición para generar las agregaciones.  
  
 Las particiones remotas solo se pueden mezclar con otras particiones remotas que se hayan definido con la misma instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Si va a usar una combinación de particiones locales y remotas, una solución alternativa consiste en crear nuevas particiones que incluyan los datos combinados, eliminando las particiones que ya no use.  
  
 Para crear una partición que sea candidata para una mezcla futura, en el Asistente para particiones puede elegir la opción de copiar el diseño de agregaciones de otra de las particiones del cubo. Esto garantizará que las particiones tienen el mismo diseño de agregaciones. Cuando se mezclan, las agregaciones de la partición de origen se combinan con las agregaciones de la partición de destino.  
  
##  <a name="bkmk_Where"></a> Actualizar el origen de la partición después de mezclar particiones  
 Las particiones se segmentan por consulta, como la cláusula WHERE de una consulta SQL usada para procesar los datos, o por una tabla o una consulta con nombre que proporcione los datos a la partición. La propiedad **Source** de la partición indica si la partición está enlazada a una consulta o una tabla.  
  
 Cuando se mezclan particiones, el contenido de las particiones se consolida, pero la propiedad **Source** no se actualiza para reflejar el ámbito adicional de la partición. Esto significa que si vuelve a procesar posteriormente una partición que conserva su valor **Source**original, obtendrá datos incorrectos de esa partición. La partición agregará erróneamente datos en el nivel primario. En el ejemplo siguiente se ilustra este comportamiento.  
  
 **El problema**  
  
 Imagine que tiene un cubo que contiene información sobre tres productos de refrescos. Tiene tres particiones que usan la misma tabla de hechos. Estas particiones están segmentadas por producto. La partición 1 contiene datos sobre [ColaFull], la partición 2 contiene datos sobre [ColaDecaf] y la partición 3 contiene datos sobre [ColaDiet]. Si la partición 3 se mezcla en la partición 2, los datos de la partición resultante (partición 2) serán correctos y los datos del cubo serán precisos. Sin embargo, cuando se procesa la partición 2, su contenido puede verse determinado por el miembro primario en el nivel del producto. Este elemento primario, [SoftDrinks], también incluye [ColaFull], el producto de la partición 1. El procesamiento de la partición 2 carga en la partición datos para todos los refrescos, incluido [ColaFull]. El cubo contendrá datos duplicados para [ColaFull] y devolverá datos incorrectos a los usuarios finales.  
  
 **Solución**  
  
 La solución consiste en actualizar la propiedad **Source** , ajustando la cláusula WHERE o la consulta con nombre, o mezclando manualmente los datos de las tablas de hechos subyacentes, para asegurarse de que el procesamiento posterior es preciso dado el ámbito ampliado de la partición.  
  
 En este ejemplo, después de mezclar la partición 3 en la partición 2, puede proporcionar un filtro como ("Product" = 'ColaDecaf' OR "Product" = 'ColaDiet') en la partición 2 resultante para especificar que únicamente se extraigan de la tabla de hechos los datos sobre [ColaDecaf] y [ColaDiet], y se excluyan los datos relacionados con [ColaFull]. Como alternativa, puede especificar filtros para la partición 2 y la partición 3 cuando se crean. Estos filtros se combinarán durante el proceso de mezcla. En cualquier caso, después de procesar la partición, el cubo no contendrá datos duplicados.  
  
 **La cConclusión**  
  
 Después de mezclar particiones, compruebe siempre **Source** para comprobar si el filtro es correcto para los datos mezclados. Si empezó con una partición que incluía datos históricos para T1, T2 y Q3, y ahora mezcla T4, debe ajustar el filtro para incluir T4. De lo contrario, el procesamiento posterior de la partición producirá resultados erróneos. No será correcto para T4.  
  
##  <a name="bkmk_fact"></a> Consideraciones especiales para las particiones segmentadas por una tabla de hechos o por una consulta con nombre  
 Además de por consultas, las particiones también se pueden segmentar por tabla o por consulta con nombre. Si la partición de origen y la partición de destino emplean la misma tabla de hechos en un origen de datos o en una vista del origen de datos, la propiedad **Source** es válida después de mezclar las particiones. Especifica los datos de la tabla de hechos que son adecuados para la partición resultante. Como los hechos necesarios para la partición resultante se encuentran en la tabla de hechos, no es necesario efectuar ninguna modificación a la propiedad **Source** .  
  
 Las particiones que usan datos de varias tablas de hechos o de varias consultas con nombre requieren un trabajo adicional. Debe mezclar manualmente los hechos de la tabla de hechos de la partición de origen en la tabla de hechos de la partición de destino.  
  
 Como alternativa, puede cambiar el origen de la partición mezclada a una consulta con nombre que devuelva el contenido de dos tablas de hechos separadas. Si no realiza este paso manual, la tabla de hechos no contiene la información completa.  
  
 Por ese mismo motivo, también es necesario actualizar las particiones que obtienen datos segmentados de consultas con nombre. La partición combinada debe tener ahora una consulta con nombre que devuelva el conjunto de resultados combinado que se ha obtenido anteriormente de las distintas consultas con nombre.  
  
## <a name="partition-storage-considerations-molap"></a>Consideraciones sobre el almacenamiento de particiones: MOLAP  
 Cuando se mezclan particiones MOLAP, también se mezclan los hechos almacenados en las estructuras multidimensionales de las particiones. Como resultado, se obtiene un partición internamente completa y coherente. Sin embargo, los hechos almacenados en particiones MOLAP son copias de los hechos contenidos en la tabla de hechos. Cuando se procesa posteriormente la partición, se eliminan los hechos almacenados en la estructura multidimensional (solo en procesamientos completos y actualizaciones) y se copian los datos contenidos en la tabla de hechos tal como se especifica en el origen de datos y en el filtro de la partición. Si la partición de origen utiliza una tabla de hechos distinta de la partición de destino, se debe mezclar manualmente la tabla de hechos de la partición de origen con la tabla de hechos de la partición de destino, para asegurar que se podrá disponer de un conjunto de datos completo cuando se procese la partición resultante. Esto se aplica también si las dos particiones se basan en consultas con nombre diferentes.  
  
> [!IMPORTANT]  
>  Una partición MOLAP mezclada con una tabla de hechos incompleta contiene una copia combinada internamente de los datos de la tabla de hechos, y funciona correctamente hasta que se procesa.  
  
## <a name="partition-storage-considerations-holap-and-rolap-partitions"></a>Consideraciones sobre el almacenamiento de particiones: particiones HOLAP y ROLAP  
 Cuando se mezclan particiones HOLAP o ROLAP que tienen tablas de hechos diferentes, las tablas de hechos no se mezclan automáticamente. A menos que se mezclen manualmente las tablas de hechos, la partición resultante solo podrá disponer de la tabla de hechos asociada con la partición de destino. Los hechos asociados con la partición de origen no estarán disponibles para obtener detalles en la partición resultante y, cuando se procese la partición, las agregaciones no resumirán los datos procedentes de la tabla no disponible.  
  
> [!IMPORTANT]  
>  Una partición HOLAP o ROLAP mezclada con una tabla de hechos incompleta contiene agregaciones precisas, pero hechos incompletos. Las consultas que hagan referencia a hechos que faltan devuelven datos incorrectos. Cuando se procesa la partición, solo se calculan las agregaciones de los hechos disponibles.  
  
 Puede que no se detecte la ausencia de hechos no disponibles a menos que un usuario intente obtener detalles de un hecho contenido en una tabla no disponible o que ejecute una consulta que requiera un hecho de la tabla no disponible. Debido a que las agregaciones se combinan durante el proceso de mezcla, las consultas cuyos resultados se basan únicamente en agregaciones devolverán datos precisos, mientras que otras consultas pueden devolver datos inexactos. Incluso después de que se procese la partición resultante, puede pasar inadvertida la pérdida de datos correspondientes a la tabla de hechos no disponible, especialmente si estos datos representan solo una pequeña parte de los datos combinados.  
  
 Las tablas de hechos se pueden mezclar antes o después de mezclar las particiones. Sin embargo, las agregaciones no representarán con precisión los hechos subyacentes hasta que hayan finalizado ambas operaciones. Se recomienda mezclar las particiones HOLAP o ROLAP que tienen acceso a diferentes tablas de hechos cuando no haya ningún usuario conectado al cubo que contiene esas particiones.  
  
##  <a name="bkmk_partitionSSMS"></a> Cómo mezclar particiones mediante SSMS  
  
> [!IMPORTANT]  
>  Antes de mezclar particiones, copie primero la información de filtro de datos (a menudo, la cláusula WHERE para los filtros basados en consultas SQL). Posteriormente, una vez completada la mezcla, debe actualizar la propiedad Origen de la partición que contiene los datos de hechos acumulados.  
  
1.  En el Explorador de objetos, expanda el nodo **Grupos de medida** del cubo que contiene las particiones que quiere mezclar, expanda **Particiones**y haga clic con el botón derecho en la partición de destino o en el destino de la operación de mezcla. Por ejemplo, si va a mover datos de hechos trimestrales a una partición que almacena datos de hechos anuales, seleccione la partición que contiene los datos de hechos anuales.  
  
2.  Haga clic en **particiones de mezcla** para abrir el **partición de mezcla \<nombre de partición >** cuadro de diálogo.  
  
3.  En **Particiones de origen**, active la casilla situada junto a cada partición de origen que desee mezclar con la partición de destino y haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Las particiones de origen se eliminan inmediatamente después de mezclarse el origen en la partición de destino. Actualice la carpeta de particiones para actualizar su contenido una vez completada la mezcla.  
  
4.  Haga clic con el botón derecho en la partición que contiene los datos acumulados y seleccione **Propiedades**.  
  
5.  Abra la propiedad **Origen** y modifique la cláusula WHERE para que incluya los datos de la partición recién mezclados. Recuerde que la propiedad **Origen** no se actualiza automáticamente. Si vuelve a procesar sin actualizar primero **Origen**, es posible que no obtenga todos los datos esperados.  
  
##  <a name="bkmk_partitionsXMLA"></a> Cómo mezclar particiones mediante XMLA  
 Para más información, vea el tema [Mezclar particiones &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Procesar objetos de Analysis Services](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)   
 [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [Crear y administrar una partición remota &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Establecer la reescritura de particiones](../../analysis-services/multidimensional-models/set-partition-writeback.md)   
 [Particiones habilitadas para escritura](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Configurar el almacenamiento de cadenas para dimensiones y particiones](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md)  
  
  

