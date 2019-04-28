---
title: Para los modelos Bayes Naive contenido del modelo de minería de datos (Analysis Services - minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- mining model content, naive bayes models
ms.assetid: 63fa15b0-e00c-4aa3-aa49-335f5572ff7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 378f59e4cf37328178cc537fde4c797badc927f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733617"
---
# <a name="mining-model-content-for-naive-bayes-models-analysis-services---data-mining"></a>Contenido del modelo de minería de datos para los modelos Bayes naive (Analysis Services - Minería de datos)
  En este tema se describe el contenido del modelo de minería de datos específico de los modelos que utilizan el algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener una explicación de cómo interpretar las estadísticas y la estructura compartidas por todos los tipos de modelos, así como las definiciones generales de los términos relacionados con el contenido del modelo de minería de datos, vea [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-naive-bayes-model"></a>Descripción de la estructura de un modelo Bayes naive  
 Un modelo Bayes naive tiene un nodo primario único que representa el modelo y sus metadatos, y debajo de dicho nodo, varios árboles independientes que representan los atributos de predicción seleccionados. Además de los árboles para los atributos, cada modelo contiene un nodo de estadísticas marginales (NODE_TYPE = 26) que proporciona estadísticas descriptivas sobre el conjunto de casos de entrenamiento. Para obtener más información, vea [Información en el nodo de estadísticas marginales](#bkmk_margstats).  
  
 Para cada atributo de predicción y valor, el modelo genera un árbol que contiene información que describe cómo afectaron las columnas de entrada al resultado de ese atributo de predicción concreto. Cada árbol contiene el atributo de predicción y su valor (NODE_TYPE = 9) y, a continuación, una serie de nodos que representan los atributos de entrada (NODE_TYPE = 10). Dado que los atributos de entrada normalmente tienen varios valores, cada uno de dichos atributos (NODE_TYPE = 10) puede tener varios nodos secundarios (NODE_TYPE = 11), uno para cada estado específico del atributo.  
  
> [!NOTE]  
>  Dado que un modelo Bayes naive no admite tipos de datos continuos, todos los valores de las columnas de entrada se tratan como discretos o discretizados. Si lo desea, puede especificar cómo se discretiza un valor. Para obtener más información, vea [Cambiar la discretización de una columna en un modelo de minería de datos](change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 ![estructura del contenido del modelo de bayes naive](../media/modelcontentstructure-nb.gif "estructura del contenido del modelo de bayes naive")  
  
## <a name="model-content-for-a-naive-bayes-model"></a>Contenido del modelo para un modelo Bayes naive  
 En esta sección solo se proporcionan detalles y ejemplos de las columnas del contenido del modelo de minería de datos que tienen una relevancia especial para los modelos Bayes naive.  
  
 Para obtener información sobre las columnas de uso general en el conjunto de filas de esquema, como MODEL_CATALOG y MODEL_NAME (que no se describen aquí), o para obtener una explicación de la terminología del modelo de minería de datos, vea [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nombre de la base de datos en la que se almacena el modelo.  
  
 MODEL_NAME  
 Nombre del modelo.  
  
 ATTRIBUTE_NAME  
 Nombres de los atributos que corresponden a este nodo.  
  
 **Raíz del modelo** : nombre del atributo de predicción.  
  
 **Estadísticas marginales** : no aplicable.  
  
 **Atributo de predicción** : nombre del atributo de predicción.  
  
 **Atributo de entrada** : nombre del atributo de entrada.  
  
 **Estado de atributo de entrada** : solo el nombre del atributo de entrada. Para obtener el estado, use MSOLAP_NODE_SHORT_CAPTION.  
  
 NODE_NAME  
 Nombre del nodo.  
  
 Esta columna contiene el mismo valor que NODE_UNIQUE_NAME.  
  
 Para obtener más información sobre las convenciones de nomenclatura de nodos, vea [Usar nombres de nodo e identificadores](#bkmk_nodenames).  
  
 NODE_UNIQUE_NAME  
 Nombre único del nodo. Los nombres únicos se asignan según una convención que proporciona información sobre las relaciones entre los nodos. Para obtener más información sobre las convenciones de nomenclatura de nodos, vea [Usar nombres de nodo e identificadores](#bkmk_nodenames).  
  
 NODE_TYPE  
 Un modelo Bayes naive genera los tipos de nodos siguientes:  
  
|Identificador del tipo de nodo|Descripción|  
|------------------|-----------------|  
|26 (NaiveBayesMarginalStatNode)|Contiene estadísticas que describen el conjunto completo de casos de entrenamiento para el modelo.|  
|9 (atributo de predicción)|Contiene el nombre del atributo de predicción.|  
|10 (atributo de entrada)|Contiene el nombre de una columna de atributos de entrada, así como nodos secundarios que contienen los valores para el atributo.|  
|11 (estado de atributo de entrada)|Contiene los valores o los valores de datos discretos de todos los atributos de entrada que se emparejaron con un atributo de salida determinado.|  
  
 NODE_CAPTION  
 Etiqueta o título asociado al nodo. Esta propiedad se usa principalmente para la presentación.  
  
 **Raíz del modelo** : en blanco.  
  
 **Estadísticas marginales** : en blanco.  
  
 **Atributo de predicción** : nombre del atributo de predicción.  
  
 **Atributo de entrada** : nombre del atributo de predicción y del atributo de entrada actual. Ej.:  
  
 Bike Buyer -> Age  
  
 **Estado de atributo de entrada** : nombre del atributo de predicción y del atributo de entrada actual, más el valor de la entrada. Ej.:  
  
 Bike Buyer -> Age = Missing  
  
 CHILDREN_CARDINALITY  
 Número de elementos secundarios que tiene el nodo.  
  
 **Raíz del modelo** : recuento de los atributos de predicción del modelo, más 1 para el nodo de estadísticas marginales.  
  
 **Estadísticas marginales** : por definición, no tiene elementos secundarios.  
  
 **Atributo de predicción**  : recuento de los atributos de entrada que estaban relacionados con el atributo de predicción actual.  
  
 **Atributo de entrada** : recuento de los valores discretos o discretizados para el atributo de entrada actual.  
  
 **Estado de atributo de entrada** : siempre es 0.  
  
 PARENT_UNIQUE_NAME  
 Nombre único del nodo primario. Para obtener más información sobre cómo relacionar nodos primarios y secundarios, vea [Usar nombres de nodo e identificadores](#bkmk_nodenames).  
  
 NODE_DESCRIPTION  
 Coincide con el título del nodo.  
  
 NODE_RULE  
 Representación XML del título del nodo.  
  
 MARGINAL_RULE  
 Coincide con la regla del nodo.  
  
 NODE_PROBABILITY  
 Probabilidad asociada a este nodo.  
  
 **Raíz del modelo** : siempre es 0.  
  
 **Estadísticas marginales** : siempre es 0.  
  
 **Atributo de predicción**  : siempre es 1.  
  
 **Atributo de entrada** : siempre es 1.  
  
 **Estado de atributo de entrada** : número decimal que representa la probabilidad del valor actual. Los valores de todos los estados de los atributos de entrada bajo el nodo de atributo de entrada primario suman 1.  
  
 MARGINAL_PROBABILITY  
 Coincide con la probabilidad del nodo.  
  
 NODE_DISTRIBUTION  
 Tabla que contiene el histograma de probabilidad del nodo. Para obtener más información vea [Tabla NODE_DISTRIBUTION](#bkmk_nodedist).  
  
 NODE_SUPPORT  
 Número de casos que admiten este nodo.  
  
 **Raíz del modelo** : recuento de todos los casos de los datos de entrenamiento.  
  
 **Estadísticas marginales** : siempre es 0.  
  
 **Atributo de predicción** : recuento de todos los casos de los datos de entrenamiento.  
  
 **Atributo de entrada** : recuento de todos los casos de los datos de entrenamiento.  
  
 **Estado de atributo de entrada** : recuento de los casos de los datos de entrenamiento que solo contienen este valor concreto.  
  
 MSOLAP_MODEL_COLUMN  
 Etiqueta que se utiliza para la visualización. Normalmente, coincide con ATTRIBUTE_NAME.  
  
 MSOLAP_NODE_SCORE  
 Representa la importancia del atributo o valor dentro del modelo.  
  
 **Raíz del modelo** Siempre es 0.  
  
 **Estadísticas marginales** : siempre es 0.  
  
 **Atributo de predicción**  : siempre es 0.  
  
 **Atributo de entrada** : Puntuación interestingness para el atributo de entrada actual en relación con el atributo de predicción actual.  
  
 **Estado de atributo de entrada** : siempre es 0.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Cadena de texto que representa el nombre o el valor de una columna.  
  
 **Raíz del modelo** : en blanco.  
  
 **Estadísticas marginales** : en blanco.  
  
 **Atributo de predicción**  : nombre del atributo de predicción.  
  
 **Atributo de entrada** : nombre del atributo de entrada.  
  
 **Estado de atributo de entrada** : valor o valor de datos discretos del atributo de entrada.  
  
##  <a name="bkmk_nodenames"></a> Usar nombres de nodo e identificadores  
 La denominación de los nodos en un modelo Bayes naive proporciona información adicional sobre el tipo de nodo, lo que facilita la comprensión de las relaciones entre los tipos de información del modelo. En la tabla siguiente se muestra la convención para los identificadores asignados a los distintos tipos de nodos.  
  
|Tipo de nodo|Convención para el identificador de nodo|  
|---------------|----------------------------|  
|Raíz del modelo (1)|Siempre es 0.|  
|Nodo de estadísticas marginales (26)|Un valor de identificador arbitrario.|  
|Atributo de predicción (9)|Número hexadecimal a partir de 10000000.<br /><br /> Ejemplo: 100000001, 10000000b|  
|Atributo de entrada (10)|Un número hexadecimal de dos partes en el que la primera siempre es 20000000, y la segunda comienza con el identificador hexadecimal del atributo de predicción relacionado.<br /><br /> Ejemplo: 20000000b00000000<br /><br /> En este caso, el atributo de predicción relacionado es 10000000b.|  
|Estado de atributo de entrada (11)|Un número hexadecimal de tres partes en el que la primera siempre es 30000000, la segunda comienza con el identificador hexadecimal del atributo de predicción relacionado y la tercera representa el identificador del valor.<br /><br /> Ejemplo: 30000000b00000000200000000<br /><br /> En este caso, el atributo de predicción relacionado es 10000000b.|  
  
 Puede usar los identificadores para relacionar los atributos de entrada y sus estados con un atributo de predicción. Por ejemplo, la consulta siguiente devuelve los nombres y los títulos de los nodos que representan las posibles combinaciones de atributos de entrada y de predicción para el modelo `TM_NaiveBayes`.  
  
```  
SELECT NODE_NAME, NODE_CAPTION  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
```  
  
 Resultados esperados:  
  
|NODE_NAME|NODE_CAPTION|  
|----------------|-------------------|  
|20000000000000001|Bike Buyer -> Commute Distance|  
|20000000000000002|Bike Buyer -> English Education|  
|20000000000000003|Bike Buyer -> English Occupation|  
|20000000000000009|Bike Buyer -> Marital Status|  
|2000000000000000a|Bike Buyer -> Number Children At Home|  
|2000000000000000b|Bike Buyer -> Region|  
|2000000000000000c|Bike Buyer -> Total Children|  
  
 A continuación, puede usar los identificadores de los nodos primarios para recuperar los nodos secundarios. La consulta siguiente recupera los nodos que contienen valores para el atributo `Marital Status` , junto con la probabilidad de cada nodo.  
  
```  
SELECT NODE_NAME, NODE_CAPTION, NODE_PROBABILITY  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 11  
AND [PARENT_UNIQUE_NAME] = '20000000000000009'  
```  
  
> [!NOTE]  
>  El nombre de la columna, PARENT_UNIQUE_NAME, debe ir entre corchetes para distinguirla de la palabra clave reservada con la misma denominación.  
  
 Resultados esperados:  
  
|NODE_NAME|NODE_CAPTION|NODE_PROBABILITY|  
|----------------|-------------------|-----------------------|  
|3000000000000000900000000|Bike Buyer -> Marital Status = Missing|0|  
|3000000000000000900000001|Bike Buyer -> Marital Status = S|0.457504004|  
|3000000000000000900000002|Bike Buyer -> Marital Status = M|0.542495996|  
  
##  <a name="bkmk_nodedist"></a> Tabla NODE_DISTRIBUTION  
 La columna de tabla anidada, NODE_DISTRIBUTION, normalmente contiene estadísticas sobre la distribución de los valores en el nodo. En un modelo Bayes naive, esta tabla se rellena solo para los nodos siguientes:  
  
|Tipo de nodo|Contenido de la tabla anidada|  
|---------------|-----------------------------|  
|Raíz del modelo (1)|: en blanco.|  
|Nodo de estadísticas marginales (24)|Contiene información de resumen para todos los atributos de predicción y de entrada, para el conjunto completo de datos de entrenamiento.|  
|Atributo de predicción (9)|: en blanco.|  
|Atributo de entrada (10)|: en blanco.|  
|Estado de atributo de entrada (11)|Contiene estadísticas que describen la distribución de los valores de los datos de entrenamiento para esta combinación concreta de un valor de predicción y un valor de atributo de entrada.|  
  
 Puede usar los identificadores de nodo o los títulos de nodo para recuperar un mayor nivel de detalle. Por ejemplo, la consulta siguiente recupera columnas concretas de la tabla NODE_DISTRIBUTION solo para aquellos nodos de atributo de entrada que están relacionados con el valor `'Marital Status = S'`.  
  
```  
SELECT FLATTENED NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM TM_NaiveBayes.content  
WHERE NODE_TYPE = 11  
AND NODE_CAPTION = 'Bike Buyer -> Marital Status = S'  
```  
  
 Resultados esperados:  
  
|NODE_CAPTION|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-------------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Bike Buyer -> Marital Status = S|Bike Buyer|Missing|0|0|1|  
|Bike Buyer -> Marital Status = S|Bike Buyer|0|3783|0.472934117|4|  
|Bike Buyer -> Marital Status = S|Bike Buyer|1|4216|0.527065883|4|  
  
 En estos resultados, el valor de la columna SUPPORT le indica el recuento de clientes con el estado civil especificado que compraron una bicicleta. La columna PROBABILITY contiene la probabilidad de cada valor de atributo, calculada solo para este nodo. Para obtener definiciones generales de los términos usados en la tabla NODE_DISTRIBUTION, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="bkmk_margstats"></a> Información en el nodo de estadísticas marginales  
 En un modelo Bayes naive, la tabla anidada para el nodo de estadísticas marginales contiene la distribución de los valores para el conjunto completo de datos de entrenamiento. Por ejemplo, la tabla siguiente contiene una lista parcial de las estadísticas de la tabla anidada NODE_DISTRIBUTION para el modelo `TM_NaiveBayes`:  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|Support|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Marital Status|Missing|0|0|0|1|  
|Marital Status|S|7999|0.457504004|0|4|  
|Marital Status|M|9485|0.542495996|0|4|  
|Total Children|Missing|0|0|0|1|  
|Total Children|0|4865|0.278254404|0|4|  
|Total Children|3|2093|0.119709449|0|4|  
|Total Children|1|3406|0.19480668|0|4|  
  
 La columna `Bike Buyer` se incluye porque el nodo de estadísticas marginales siempre contiene una descripción del atributo de predicción y sus valores posibles. El resto de columnas incluidas representan atributos de entrada, junto con los valores que se usaron en el modelo. Los valores solo pueden ser ausentes, discretos o discretizados.  
  
 En un modelo Bayes naive, no puede haber atributos continuos; por lo tanto, todos los datos numéricos se representan como discretos (VALUE_TYPE = 4) o discretizados (VALUE_TYPE = 5).  
  
 Se agrega un valor `Missing` (VALUE_TYPE = 1) a cada atributo de entrada y de salida para representar valores potenciales que no estaban presentes en los datos de entrenamiento. Debe tener cuidado de distinguir entre "missing" como cadena y el valor `Missing` predeterminado. Para más información, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](missing-values-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)   
 [Consultas de minería de datos](data-mining-queries.md)   
 [Algoritmo Bayes naive de Microsoft](microsoft-naive-bayes-algorithm.md)  
  
  
