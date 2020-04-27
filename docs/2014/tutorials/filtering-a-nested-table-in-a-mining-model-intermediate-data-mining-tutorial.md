---
title: Filtrar una tabla anidada en un modelo de minería de datos (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f57d691587d658e968cd79cf4f4ab4731db29915
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63267478"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>Filtrar un tabla anidada en un modelo de minería de datos (tutorial intermedio de minería de datos)
  Una vez creado y explorado el modelo, tal vez decida centrarse en un subconjunto de datos del cliente. Por ejemplo, es posible que solo desee analizar las cestas que contienen un producto específico o los datos demográficos de los clientes que no han realizado ninguna compra en un determinado período.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona la capacidad de filtrar los datos que se emplean en un modelo de minería de datos. Esta característica es útil porque no es necesario configurar una nueva vista del origen de datos para utilizar datos diferentes. En el Tutorial básico de minería de datos aprendió a filtrar datos de una tabla plana aplicando condiciones a la tabla de casos. En esta tarea, creará un filtro que se aplica a una tabla anidada.  
  
## <a name="filters-on-nested-vs-case-tables"></a>Comparación de los filtros en tablas anidadas y en tablas de casos  
 Si la vista del origen de datos contiene una tabla de casos y una tabla anidada, como la vista del origen de datos utilizada en el modelo de asociación, puede filtrar valores de la tabla de casos, comprobar la presencia o ausencia de un valor en la tabla anidada o alguna combinación de ambos.  
  
 En esta tarea, primero realizará una copia del modelo de asociación y, a continuación, agregará los atributos IncomeGroup y Region al nuevo modelo relacionado, para que pueda crear un filtro a partir de esos atributos en la tabla de casos.  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>Para crear y modificar una copia del modelo Association  
  
1.  En la **pestaña modelos de minería de datos** de, haga `Association` clic con el botón secundario en el modelo y seleccione **nuevo modelo de minería**de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]datos.  
  
2.  En **nombre del modelo**, `Association Filtered`escriba. En **nombre del algoritmo**, seleccione **reglas de Asociación de Microsoft**. Haga clic en **Aceptar**.  
  
3.  En la columna del modelo de asociación filtrado, haga clic en la fila IncomeGroup y cambie el valor de **omitir** a **entrada**.  
  
 A continuación, creará un filtro para la tabla de casos en el nuevo modelo de asociación. El filtro pasará al modelo solo los clientes de la región de destino o con el nivel de ingresos de destino. A continuación, agregará un segundo conjunto de condiciones de filtro para especificar que el modelo utilice solo los clientes cuyas cestas de la compra contengan al menos un producto.  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>Para agregar un filtro a un modelo de minería de datos  
  
1.  En la pestaña **modelos de minería de datos** , haga clic con el botón secundario en la Asociación de modelo filtrada y seleccione **establecer filtro de modelos**.  
  
2.  En el cuadro de diálogo **Filtro del modelo** , haga clic en la fila superior de la cuadrícula en el cuadro de texto **Columna de la estructura de minería de datos** .  
  
3.  En el cuadro de texto columna de la **estructura de minería de datos** , seleccione IncomeGroup.  
  
     El icono situado en la parte izquierda del cuadro de texto cambia para indicar que el elemento seleccionado es una columna.  
  
4.  Haga clic **Operator** en el cuadro de texto operador **=** y seleccione el operador de la lista.  
  
5.  Haga clic **Value** en el cuadro de texto valor `High` y escriba en el cuadro.  
  
6.  Haga clic en la siguiente fila de la cuadrícula.  
  
7.  Haga clic en el cuadro de texto **y/o** de la siguiente fila de la cuadrícula y seleccione **o**.  
  
8.  En el cuadro de texto columna de la **estructura de minería de datos** , seleccione IncomeGroup. En el cuadro de texto **valor** , `Moderate`escriba.  
  
     La condición de filtro que ha creado se agrega automáticamente al cuadro de texto **expresión** y debe aparecer de la siguiente manera:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. Haga clic en la siguiente fila de la cuadrícula, manteniendo el operador como predeterminado, **y**.  
  
10. Para **operador**, deje el valor predeterminado, **Contains**. Haga clic en el cuadro de texto **valor** .  
  
11. En el cuadro de diálogo **filtro** , en la primera fila de la **columna estructura de minería de datos**, seleccione `Model`.  
  
12. Para **operador**, seleccione **no es null**. Deje en blanco el cuadro de texto **valor** . Haga clic en **Aceptar**.  
  
     La condición de filtro del cuadro de texto **expresión** del cuadro de diálogo **filtro del modelo** se actualiza automáticamente para incluir la nueva condición en la tabla anidada. La expresión completa es la siguiente:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>Para habilitar la obtención de detalles y procesar el modelo filtrado  
  
1.  En la pestaña **modelos de minería de datos** , haga `Association Filtered` clic con el botón secundario en el modelo y seleccione **propiedades**.  
  
2.  Cambie la propiedad **AllowDrillThrough** a **true**.  
  
3.  Haga clic con el `Association Filtered` botón secundario en el modelo de minería de datos y seleccione **procesar modelo**.  
  
4.  Haga clic en **sí** en el mensaje de error para implementar el nuevo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] modelo en la base de datos.  
  
5.  En el cuadro de diálogo **procesar estructura de minería de datos** , haga clic en **Ejecutar**.  
  
6.  Cuando se haya completado el procesamiento, haga clic en **cerrar** para salir del cuadro de diálogo **progreso del proceso** y haga clic de nuevo en **cerrar** para salir del cuadro de diálogo **procesar estructura de minería de datos** .  
  
 Mediante el Visor de árbol de contenido genérico de Microsoft y examinando el valor de NODE_SUPPORT, puede comprobar que el modelo filtrado contiene menos casos que el modelo original.  
  
## <a name="remarks"></a>Observaciones  
 El filtro de tabla anidada que acaba de crear solo comprueba la presencia de al menos una fila en la tabla anidada; no obstante, puede crear condiciones de filtro que comprueben la existencia de productos específicos.  Por ejemplo, podría crear el siguiente filtro:  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 Esta instrucción restringe los clientes de la tabla de casos a solo aquellos que han comprado una botella de agua. Sin embargo, dado que el número de atributos de tabla anidada es potencialmente ilimitado, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no suministra ninguna lista de valores posibles entre los que seleccionar. En lugar de ello, debe escribir el valor exacto.  
  
 Puede hacer clic en **Editar consulta** para cambiar manualmente la expresión de filtro. Sin embargo, si cambia manualmente una parte de la expresión de filtro, la cuadrícula estará deshabilitada y a partir de este momento deberá trabajar solo con la expresión de filtro en modo de edición de texto. Para restaurar el modo de edición de cuadrícula, debe borrar la expresión de filtro y comenzar de nuevo.  
  
> [!WARNING]  
>  No se puede usar el operador LIKE en un filtro de tabla anidada.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Predicción de asociaciones &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Sintaxis y ejemplos del filtro de modelos &#40;Analysis Services:&#41;de minería de datos](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
