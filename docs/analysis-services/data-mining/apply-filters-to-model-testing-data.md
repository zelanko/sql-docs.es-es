---
title: Aplicar filtros para modelar los datos de prueba | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae4d7899d0b027f912b6320934ddefc2431a303a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="apply-filters-to-model-testing-data"></a>Aplicar filtros a los datos de prueba del modelo
  Al especificar un origen de datos externo que se va a utilizar para probar un modelo, opcionalmente puede aplicar un filtro para restringir los datos de entrada. Por ejemplo, es posible que desee probar el modelo específicamente para realizar predicciones para los clientes con a un intervalo de ingresos determinado.  
  
 Por ejemplo, en el escenario de distribución de correo directo de Adventure Works, puede crear una expresión de filtro como la siguiente en ProspectiveBuyer, que es la tabla que contiene los datos de prueba, y restringir los casos por intervalo de ingresos:  
  
 `[YearlyIncome] = '50000'`  
  
 El comportamiento de los filtros es ligeramente diferente, dependiendo de si se filtran datos del entrenamiento del modelo o un conjunto de datos de prueba:  
  
-   Al definir un filtro en un conjunto de datos de prueba, realmente está creando una cláusula WHERE en los datos de entrada. Si está filtrando un conjunto de datos de entrada que se usa para evaluar un modelo, la expresión del filtro se traduce a una instrucción de Transact-SQL y se aplica a la tabla de entrada en el momento de crear el gráfico. Como resultado, se puede reducir en gran medida el número de casos de prueba.  
  
-   Al aplicar un filtro a un modelo de minería de datos, la expresión del filtro que cree se traducirá a una instrucción de Extensiones de minería de datos (DMX) y se aplicará al modelo individual. Por lo tanto, al aplicar un filtro a un modelo, solamente se utilizará un subconjunto de los datos originales para entrenar el modelo. Esto puede causar problemas si se filtra el modelo de entrenamiento con un conjunto de criterios, de tal forma que el modelo se ajuste a cierto conjunto de datos, y, a continuación, se prueba el modelo con otro conjunto de criterios.  
  
-   Si define un conjunto de datos de pruebas en el momento de crear la estructura, entre los casos del modelo utilizados para el entrenamiento solamente se incluyen los que se encuentran en el conjunto de entrenamiento de la estructura de minería de datos **y** que cumplen con las condiciones del filtro. De este modo, al probar un modelo y seleccionar la opción **Usar casos de prueba de modelo de minería de datos**, entre los casos de prueba solamente se incluirán los que se encuentran en el conjunto de prueba de la estructura de minería de datos y que cumplen las condiciones del filtro. Sin embargo, si no definió un conjunto de datos de exclusiones, en los casos del modelo utilizados para la prueba se incluyen todos los casos del conjunto de datos que cumplan las condiciones de filtro.  
  
-   Las condiciones de filtro que se apliquen en un modelo también afectarán a las consultas de obtención de detalles en los casos del modelo.  
  
 En resumen, cuando se prueban varios modelos, aunque todos estén basados en la misma estructura de minería de datos, se debe tener en cuenta que es posible que los modelos utilicen subconjuntos de datos diferentes para el entrenamiento y las pruebas. Esto puede tener los efectos siguientes en los gráficos de precisión:  
  
-   El número total de casos en los conjuntos de pruebas puede variar entre los modelos que se prueban.  
  
-   Es posible que los porcentajes para cada modelo no estén alineados en el gráfico si los modelos utilizan subconjuntos de datos de entrenamiento o de prueba diferentes.  
  
 Para determinar si un modelo contiene un filtro predefinido que puede afectar a los resultados, busque la propiedad **Filter** en el panel **Propiedad** o consulte el modelo utilizando los conjuntos de filas de esquema de minería de datos. Por ejemplo, la consulta siguiente devuelve el texto del filtro para el modelo especificado:  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  Si desea quitar el filtro de un modelo de minería de datos existente, o cambiar las condiciones del filtro, deberá volver a procesar dicho modelo.  
  
 Para más información sobre los tipos de filtros que se pueden aplicar y cómo se evalúan las expresiones de filtro, vea [Sintaxis y ejemplos del filtro de modelos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
### <a name="create-a-filter-on-external-testing-data"></a>Crear un filtro en datos de prueba externos  
  
1.  Haga doble clic en la estructura de minería de datos que contiene el modelo que desea probar para abrir el Diseñador de minería de datos.  
  
2.  Seleccione la pestaña **Gráfico de precisión de minería de datos** y luego seleccione la pestaña **Selección de entrada** .  
  
3.  En la pestaña **Selección de entrada** , en **Seleccionar un conjunto de datos para usarlo en un gráfico de precisión**, seleccione la opción **Especificar otro conjunto de datos**.  
  
4.  Haga clic en el botón Examinar **(…)** para abrir un cuadro de diálogo y seleccionar el conjunto de datos externo.  
  
5.  Elija la tabla de casos y agregue una tabla anidada si fuera necesario. Asigne columnas del modelo a columnas del conjunto de datos externos según sea necesario. Cierre el cuadro de diálogo **Especificar asignación de columna** para guardar la definición de la tabla de origen.  
  
6.  Haga clic en **Abrir editor de filtros** para definir un filtro para el conjunto de datos.  
  
     Aparece el cuadro de diálogo **Filtro de conjunto de datos** . Si la estructura contiene una tabla anidada, puede crear un filtro en dos partes. En primer lugar, establezca las condiciones en la tabla de casos mediante el cuadro de diálogo **Filtro de conjunto de datos** y, a continuación, establezca las condiciones en las filas anidadas mediante el cuadro de diálogo **Filtro** .  
  
7.  En el cuadro de diálogo **Filtro de conjunto de datos** , haga clic en la fila superior de la cuadrícula, en **Columna de la estructura de minería de datos**, y seleccione una tabla o columna en la lista.  
  
     Si la vista del origen de datos contiene varias tablas o una tabla anidada, debe seleccionar primero el nombre de la tabla. De lo contrario, puede seleccionar las columnas directamente en la tabla de casos.  
  
     Agregue una nueva fila para cada columna que desea filtrar.  
  
8.  Use las columnas **Operator**y **Value** para definir cómo se filtra la columna.  
  
     **Nota** : escriba los valores sin usar comillas tipográficas.  
  
9. Haga clic en el cuadro de texto **Y/O** y seleccione un operador lógico para definir cómo se combinan varias condiciones.  
  
10. También puede hacer clic en el botón Examinar **(…)** a la derecha del cuadro de texto **Valor** para abrir el cuadro de diálogo **Filtro** y establecer las condiciones en la tabla anidada o en las columnas de la tabla de casos.  
  
11. Vea el texto que aparece en el panel **Expresión** para comprobar que las condiciones de filtro completadas son correctas.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     La condición de filtro se aplica al origen de datos al crear el gráfico de precisión.  
  
## <a name="see-also"></a>Vea también  
 [Elegir y asignar datos de prueba para el modelo](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Uso de datos de tabla anidada como entrada para un gráfico de precisión](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [Elegir un tipo de gráfico de precisión y establecer opciones del gráfico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  

