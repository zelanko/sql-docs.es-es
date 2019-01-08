---
title: Agregar modelos de minería de datos a una estructura (Analysis Services - minería de datos) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3647ff06d00aebc4b5feb735d5a69b0b8db79e7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524584"
---
# <a name="add-mining-models-to-a-structure-analysis-services---data-mining"></a>Agregar modelos de minería de datos a una estructura (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una estructura de minería de datos se ha diseñado para admitir varios modelos de minería de datos. Por tanto, cuando el asistente finalice, puede abrir la estructura y agregar nuevos modelos de minería de datos. Cada vez que cree un modelo, puede utilizar un algoritmo diferente, cambiar los parámetros o aplicar filtros para utilizar un subconjunto distinto de datos.  
  
## <a name="adding-new-mining-models"></a>Agregar nuevos modelos de minería de datos  
 Si utiliza el Asistente para minería de datos para crear un nuevo modelo de minería de datos, de forma predeterminada, primero siempre debe crear una estructura de minería de datos. El asistente le ofrece la posibilidad de agregar un modelo de minería de datos inicial a la estructura. Sin embargo, no es necesario crear un modelo de manera inmediata. Si solo crea la estructura, no necesita tomar una decisión sobre qué columna debe utilizar como atributo de predicción, o sobre cómo utilizar los datos en un modelo determinado. En su lugar, solo tiene que establecer la estructura de datos general que desea utilizar en el futuro; más adelante puede utilizar [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) para agregar nuevos modelos de minería de datos basados en dicha estructura.  
  
> [!NOTE]  
>  En DMX, la instrucción CREATE MINING MODEL comienza con el modelo de minería de datos. Es decir, debe definir la opción de modelo de minería de datos que desee y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generará automáticamente la estructura subyacente. Más adelante puede seguir agregando nuevos modelos de minería de datos a esa estructura, mediante el uso de la instrucción ALTER STRUCTURE... ADD MODEL.  
  
## <a name="choosing-an-algorithm"></a>Elegir un algoritmo  
 Si agrega un modelo nuevo a una estructura existente, en primer lugar debe seleccionar un algoritmo de minería de datos para utilizarlo en el modelo. Elegir el algoritmo es importante porque cada algoritmo realiza un tipo diferente de análisis y tiene requisitos diferentes.  
  
 Si selecciona un algoritmo que sea incompatible con los datos, recibirá una advertencia. En algunos casos, puede que tenga que omitir las columnas que el algoritmo no pueda procesar. En otros casos, el algoritmo realizará automáticamente los ajustes necesarios. Por ejemplo, si la estructura contiene datos numéricos y el algoritmo solo puede trabajar con valores discretos, agrupará los valores numéricos en intervalos discretos automáticamente. En algunos casos, puede que tenga que corregir de forma manual los datos primero eligiendo una clave o un atributo de predicción.  
  
 No tiene que cambiar el algoritmo al crear un nuevo modelo. A menudo puede obtener resultados muy diferentes con el mismo algoritmo, filtrando los datos o cambiando un parámetro como el método de clústeres o el tamaño mínimo del conjunto de elementos. Se recomienda que experimente con varios modelos para comprobar qué parámetros generan los mejores resultados.  
  
 Tenga en cuenta que todos los modelos nuevos deben procesarse para poder usarse.  
  
## <a name="specifying-the-usage-of-columns-in-a-new-mining-model"></a>Especificar el uso de columnas en un modelo de minería de datos  
 Al agregar nuevos modelos de minería de datos a una estructura de minería de datos existente, debe especificar cada columna de datos que debe utilizar el modelo. Según el tipo de algoritmo que se elija para el modelo, algunas de estas opciones se pueden efectuar de forma predeterminada. Si no define un tipo de uso para una columna, esta no se incluirá en la estructura de minería de datos. Sin embargo, los datos de la columna pueden seguir disponibles para la obtención de detalles, si el modelo lo admite.  
  
 Las columnas de la estructura de minería de datos que utiliza el modelo (si no está establecido en Omitir) deben ser una clave, una columna de entrada, una columna de predicción o una columna de predicción cuyos valores también se usen como entradas en el modelo.  
  
-   Las columnas de clave contienen un único identificador para cada fila de una tabla. Algunos modelos de minería de datos, como los que se basan en la agrupación en clústeres de secuencia o en algoritmos de serie temporal, pueden contener varias columnas de clave. Sin embargo, estas claves no son claves compuestas en el sentido relacional, pero deben seleccionarse de esta forma para proporcionar soporte a las series temporales y al análisis de agrupación en clústeres de secuencia.  
  
-   Las columnas de entrada proporcionan la información desde la cual se crean las predicciones. El Asistente para minería de datos ofrece la característica **Sugerir** , que se habilita cuando se selecciona una columna de predicción. Si hace clic en este botón, el asistente muestreará los valores de predicción y determinará qué otras columnas de la estructura constituyen variables apropiadas. Rechazará las columnas de clave u otras columnas con muchos valores únicos y sugerirá columnas que parezcan tener correlación con el resultado.  
  
     Esta característica resulta especialmente práctica cuando los conjuntos de datos contienen más columnas de las que realmente se necesitan para generar un modelo de minería de datos. La característica **Sugerir** calcula una puntuación numérica, de 0 a 1, que describe la relación de cada columna del conjunto de datos con la columna de predicción. Basándose en esta puntuación, la característica sugiere las columnas que se pueden usar como entrada para el modelo de minería de datos. Si utiliza la característica **Sugerir** , puede usar las columnas sugeridas, modificar las selecciones para que se ajusten a sus necesidades o pasar por alto las sugerencias.  
  
-   Las columnas de predicción contienen la información que se intenta predecir en el modelo de minería de datos. Puede seleccionar varias columnas con los atributos de predicción. Los modelos de clústeres son la excepción, en el sentido de que un atributo de predicción es opcional.  
  
     Según el tipo de modelo, podría ser necesario que la columna de predicción fuera un tipo de datos específico: por ejemplo, un modelo de regresión lineal requiere una columna numérica como valor de predicción; el algoritmo Bayes Naïve requiere un valor discreto (y todas las entradas también deben ser discretas).  
  
## <a name="specifying-column-content"></a>Especificar el contenido de las columnas  
 Para algunas columnas, también puede ser necesario especificar el *contenido de la columna*. En la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la propiedad Tipo de contenido de cada columna de datos indica al algoritmo cómo debe procesar los datos de esa columna. Por ejemplo, si los datos tienen una columna Ingresos , debe especificar que la columna contiene números continuos estableciendo el tipo de contenido en Continuous. Sin embargo, también puede especificar que los números de la columna Ingresos se agrupen en cubos estableciendo el tipo de contenido en Discretized y, opcionalmente, especificando el número exacto de cubos. Puede crear distintos modelos que procesen las columnas de manera diferente: por ejemplo, puede probar un modelo que agrupe clientes en tres cubos en función de la edad, y otro modelo que los agrupe en 10 cubos en función de la edad.  
  
## <a name="see-also"></a>Vea también  
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Propiedades del modelo de minería de datos](../../analysis-services/data-mining/mining-model-properties.md)   
 [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md)  
  
  
