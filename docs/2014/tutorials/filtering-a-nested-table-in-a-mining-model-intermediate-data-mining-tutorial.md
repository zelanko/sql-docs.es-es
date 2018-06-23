---
title: Filtrar una tabla anidada en un modelo de minería de datos (Tutorial de minería de datos intermedios) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9b11971c6e6005c7e1d65a1728e8b8aac818b41c
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312323"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>Filtrar un tabla anidada en un modelo de minería de datos (tutorial intermedio de minería de datos)
  Una vez creado y explorado el modelo, tal vez decida centrarse en un subconjunto de datos del cliente. Por ejemplo, es posible que solo desee analizar las cestas que contienen un producto específico o los datos demográficos de los clientes que no han realizado ninguna compra en un determinado período.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona la capacidad de filtrar los datos que se emplean en un modelo de minería de datos. Esta característica es útil porque no es necesario configurar una nueva vista de origen de datos para usar datos diferentes. En el Tutorial básico de minería de datos aprendió a filtrar datos de una tabla plana aplicando condiciones a la tabla de casos. En esta tarea, creará un filtro que se aplica a una tabla anidada.  
  
## <a name="filters-on-nested-vs-case-tables"></a>Comparación de los filtros en tablas anidadas y en tablas de casos  
 Si la vista del origen de datos contiene una tabla de casos y una tabla anidada, como la vista del origen de datos utilizada en el modelo de asociación, puede filtrar valores de la tabla de casos, comprobar la presencia o ausencia de un valor en la tabla anidada o alguna combinación de ambos.  
  
 En esta tarea, primero realizará una copia del modelo de asociación y, a continuación, agregará los atributos IncomeGroup y Region al nuevo modelo relacionado, para que pueda crear un filtro a partir de esos atributos en la tabla de casos.  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>Para crear y modificar una copia del modelo Association  
  
1.  En el **modelos de minería de datos** ficha de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el `Association` de modelo y seleccione **nuevo modelo de minería de datos**.  
  
2.  Para **nombre del modelo**, tipo `Association Filtered`. Para **nombre del algoritmo**, seleccione **reglas de asociación de Microsoft**. Haga clic en **Aceptar**.  
  
3.  En la columna para el modelo de asociación filtrada, haga clic en la fila IncomeGroup y cambie el valor de **omitir** a **entrada**.  
  
 A continuación, creará un filtro para la tabla de casos en el nuevo modelo de asociación. El filtro pasará al modelo solo los clientes de la región de destino o con el nivel de ingresos de destino. A continuación, agregará un segundo conjunto de condiciones de filtro para especificar que el modelo utilice solo los clientes cuyas cestas de la compra contengan al menos un producto.  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>Para agregar un filtro a un modelo de minería de datos  
  
1.  En el **modelos de minería de datos** pestaña, haga clic en el modelo de asociación filtrada y seleccione **Establecer filtro de modelos**.  
  
2.  En el cuadro de diálogo **Filtro del modelo** , haga clic en la fila superior de la cuadrícula en el cuadro de texto **Columna de la estructura de minería de datos** .  
  
3.  En el **columna de estructura de minería de datos** cuadro de texto, seleccione IncomeGroup.  
  
     El icono situado en la parte izquierda del cuadro de texto cambia para indicar que el elemento seleccionado es una columna.  
  
4.  Haga clic en el **operador** cuadro de texto y seleccione la **=** operador de la lista.  
  
5.  Haga clic en el **valor** cuadro de texto y escriba `High` en el cuadro.  
  
6.  Haga clic en la siguiente fila de la cuadrícula.  
  
7.  Haga clic en el **o** cuadro de texto en la siguiente fila de la cuadrícula y seleccione **o**.  
  
8.  En el **columna de estructura de minería de datos** cuadro de texto, seleccione IncomeGroup. En el **valor** cuadro de texto, escriba `Moderate`.  
  
     La condición de filtro que ha creado se agrega automáticamente a la **expresión** cuadro de texto y debe aparece como sigue:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. Haga clic en la siguiente fila de la cuadrícula, dejando el operador como el valor predeterminado, **AND**.  
  
10. Para **operador**, deje el valor predeterminado, **Contains**. Haga clic en el **valor** cuadro de texto.  
  
11. En el **filtro** cuadro de diálogo, en la primera fila bajo **columna de estructura de minería de datos**, seleccione `Model`.  
  
12. Para **operador**, seleccione **IS NOT NULL**. Deje el **valor** cuadro de texto en blanco. Haga clic en **Aceptar**.  
  
     La condición de filtro en el **expresión** cuadro de texto de la **filtro del modelo** cuadro de diálogo se actualiza automáticamente para incluir la nueva condición en la tabla anidada. La expresión completa es la siguiente:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>Para habilitar la obtención de detalles y procesar el modelo filtrado  
  
1.  En el **modelos de minería de datos** pestaña, haga clic en el `Association Filtered` de modelo y seleccione **propiedades**.  
  
2.  Cambiar el **AllowDrillThrough** propiedad **True**.  
  
3.  Haga clic en el `Association Filtered` modelo de minería de datos y seleccione **modelo de proceso**.  
  
4.  Haga clic en **Sí** en el mensaje de error para implementar el nuevo modelo para el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos.  
  
5.  En el **procesar estructura de minería de datos** cuadro de diálogo, haga clic en **ejecutar**.  
  
6.  Cuando se completa el procesamiento, haga clic en **cerrar** para salir de la **progreso del proceso** cuadro de diálogo y haga clic en **cerrar** nuevo para salir del **procesar estructura de minería de datos**  cuadro de diálogo.  
  
 Mediante el Visor de árbol de contenido genérico de Microsoft y examinando el valor de NODE_SUPPORT, puede comprobar que el modelo filtrado contiene menos casos que el modelo original.  
  
## <a name="remarks"></a>Notas  
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
 [Predecir asociaciones &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [La sintaxis de filtros y ejemplos de modelos &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Filtros para modelos de minería de datos de &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  