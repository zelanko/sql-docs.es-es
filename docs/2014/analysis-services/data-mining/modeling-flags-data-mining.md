---
title: Marcas de modelado (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37263c42e4e9f37b1b782dc07b8df03f77092b14
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083307"
---
# <a name="modeling-flags-data-mining"></a>Marcas de modelado (Minería de datos)
  Puede utilizar marcas de modelado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para proporcionar información adicional a un algoritmo de minería de datos acerca de los datos que se definen en una tabla de casos. El algoritmo puede usar esta información para crear un modelo de minería de datos más preciso.  
  
 Algunas marcas de modelado se definen en la estructura de minería de datos, mientras que otras se definen en la columna del modelo de minería de datos. Por ejemplo, la marca de modelado `NOT NULL` se utiliza con las columnas de la estructura de minería de datos. Puede definir marcas de modelado adicionales en las columnas del modelo de minería de datos, dependiendo del algoritmo que se utilice para crear el modelo.  
  
> [!NOTE]  
>  Los complementos de otros proveedores podrían tener otras marcas de modelado, además de las predefinidas por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="list-of-modeling-flags"></a>Lista de marcas de modelado  
 En la lista siguiente se describen las marcas de modelado compatibles con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener información acerca de las marcas de modelado admitidas por determinados algoritmos, vea el tema de referencia técnica correspondiente al algoritmo que se usó para crear el modelo.  
  
 `NOT NULL`  
 Indica que los valores de la columna de atributos nunca deben incluir un valor NULL. Se producirá un error si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encuentra un valor NULL para esta columna de atributos durante el proceso de entrenamiento de modelos.  
  
 **MODEL_EXISTENCE_ONLY**  
 Indica que la columna se tratará como si tuviera dos estados posibles: `Missing` y `Existing`. Si el valor es `NULL`, se trata como Ausente. La marca MODEL_EXISTENCE_ONLY se aplica al atributo de predicción y es compatible con la mayoría de los algoritmos.  
  
 De hecho, al establecer la marca MODEL_EXISTENCE_ONLY en `True` se cambia la representación de los valores de forma que solo haya dos estados: `Missing` y `Existing`. Todos los estados que indica que no falta un elemento se combinan en un único valor `Existing`.  
  
 Un uso típico de esta marca de modelado se daría en los atributos para los que el estado `NULL` tiene un significado implícito; el valor explícito del estado `NOT NULL` podría no ser tan importante como el hecho de que la columna tenga cualquier valor. Por ejemplo, una columna [DateContractSigned] podría ser `NULL` si nunca se llegó a firmar el contrato y `NOT NULL` si se llegó a firmar. Por tanto, si la finalidad del modelo es predecir si se firmará el contrato, podría utilizar la marca MODEL_EXISTENCE_ONLY para omitir el valor de fecha exacto en los casos `NOT NULL` y hacer distinciones únicamente en los casos donde un contrato es `Missing` o `Existing`.  
  
> [!NOTE]  
>  Ausente es un estado especial utilizado por el algoritmo y no debe confundirse con el valor de texto "Ausente" de una columna. Para más información, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](missing-values-analysis-services-data-mining.md).  
  
 `REGRESSOR`  
 Indica que la columna es candidata para utilizarse como regresor durante el procesamiento. Esta marca se define en una columna de modelo de minería de datos y solo se puede aplicar a las columnas que tienen un tipo de datos numéricos continuo. Para más información sobre el uso de esta marca, vea en este tema la sección [Usos de la marca de modelado REGRESSOR](#bkmk_UseRegressors).  
  
## <a name="viewing-and-changing-modeling-flags"></a>Ver y cambiar marcas de modelado  
 Puede ver y modificar las marcas de modelado asociadas a una columna de un modelo o de una estructura de minería de datos en el Diseñador de minería de datos examinando las propiedades de la estructura o del modelo.  
  
 Para determinar qué marcas de modelado se han aplicado a la estructura de minería de datos actual, puede crear una consulta en el conjunto de filas de esquema de minería de datos que devuelve las marcas de modelado solo para las columnas de estructura, mediante una consulta como la siguiente:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 Puede agregar o cambiar las marcas de modelado utilizadas en un modelo mediante el Diseñador de minería de datos y modificar las propiedades de las columnas asociadas. Dichos cambios requieren que la estructura o el modelo se vuelvan a procesar.  
  
 Puede especificar las marcas de modelado en una nueva estructura o modelo de minería de datos mediante DMX, o utilizando AMO o XMLA. Sin embargo, no puede cambiar las marcas de modelado utilizadas en un modelo y en una estructura de minería de datos existentes utilizando DMX. Puede crear un nuevo modelo de minería de datos utilizando la sintaxis `ALTER MINING STRUCTURE....ADD MINING MODEL`.  
  
##  <a name="bkmk_UseRegressors"></a> Usos de la marca de modelado REGRESSOR  
 Cuando se establece la marca de modelado REGRESSOR en una columna, se indica al algoritmo que la columna contiene regresores potenciales. Los regresores reales que se utilizan en el modelo los determina el algoritmo. Se puede descartar un regresor potencial si no modela el atributo de predicción.  
  
 Cuando se genera un modelo mediante el Asistente para minería de datos, todas las columnas de entrada continuas se marcan como posibles regresores. Por tanto, aunque no establezca explícitamente la marca REGRESSOR en una columna, la columna podría utilizarse como regresor en el modelo.  
  
 Puede determinar los regresores que se utilizaron realmente en el modelo procesado realizando una consulta en el conjunto de filas de esquema para el modelo de minería de datos, tal y como se muestra en el ejemplo siguiente:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **Nota** Si modifica un modelo de minería de datos y cambia el tipo de contenido de una columna de continuo a discreto, deberá cambiar manualmente la marca en la columna de minería de datos y, a continuación, volver a procesar el modelo.  
  
### <a name="regressors-in-linear-regression-models"></a>Regresores en modelos de regresión lineal  
 Los modelos de regresión lineal se basan en el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Aun cuando no utilice el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , cualquier modelo de árbol de decisión puede contener un árbol o nodos que representen una regresión en un atributo continuo.  
  
 Por lo tanto, en estos modelos no es necesario especificar que una columna continua representa un regresor. El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] dividirá el conjunto de datos en regiones con patrones significativos aunque no establezca la marca REGRESSOR en la columna. La diferencia estriba en que, al establecer la marca de modelado, el algoritmo intentará buscar ecuaciones de regresión con el formato siguiente para ajustarlos a los patrones de los nodos del árbol.  
  
 a*C1 + b\*C2 + …  
  
 Después, se calcula la suma de los valores residuales y, si la desviación es demasiado grande, se fuerza una división en el árbol.  
  
 Por ejemplo, si está prediciendo los hábitos de compra de los clientes utilizando **Income** como atributo y ha establecido la marca de modelado REGRESSOR en la columna, el algoritmo intentará en primer lugar ajustar los valores de **Income** mediante una fórmula de regresión estándar. Si la desviación es demasiado grande, se abandona la fórmula de regresión y el árbol se dividirá de acuerdo con algún otro atributo. A continuación, el algoritmo de árboles de decisión intentará ajustar un regresor para los ingresos en cada una de las ramas después de la división.  
  
 Puede utilizar el parámetro FORCE_REGRESSOR para garantizar que el algoritmo utilizará un regresor determinado. Este parámetro se puede utilizar con el algoritmo de árboles de decisión y el algoritmo de regresión lineal.  
  
## <a name="related-tasks"></a>Related Tasks  
 Utilice los vínculos siguientes para obtener más información acerca de cómo utilizar marcas de modelado.  
  
|Tarea|Tema|  
|----------|-----------|  
|Modificar las marcas de modelado mediante el Diseñador de minería de datos|[Ver o cambiar marcas de modelado &#40;minería de datos&#41;](modeling-flags-data-mining.md)|  
|Especificar una sugerencia al algoritmo para recomendar regresores probables|[Especificar una columna para usar como regresor en un modelo](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Ver las marcas de modelado admitidas por algoritmos concretos (en la sección Marcas de modelado de cada tema de referencia del algoritmo)|[Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)|  
|Obtener más información acerca de las columnas de la estructura de minería de datos y las propiedades que se pueden establecer en ellas|[Columnas de la estructura de minería de datos](mining-structure-columns.md)|  
|Obtener información sobre las marcas de modelado y las columnas del modelo de minería de datos que se pueden aplicar en el modelo|[Columnas del modelo de minería de datos](mining-model-columns.md)|  
|Ver la sintaxis para trabajar con marcas de modelado en instrucciones DMX|[Marcas de modelado &#40;DMX&#41;](/sql/dmx/modeling-flags-dmx)|  
|Descripción de los valores que faltan y cómo trabajar con ellos|[Valores ausentes &#40;Analysis Services - Minería de datos&#41;](missing-values-analysis-services-data-mining.md)|  
|Obtener información sobre cómo administrar los modelos y las estructuras y establecer las propiedades de uso|[Mover objetos de minería de datos](moving-data-mining-objects.md)|  
  
  
