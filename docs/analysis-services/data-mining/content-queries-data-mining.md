---
title: "Consultas (minería de datos) de contenido | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4f4a5a8-a230-4222-bece-9d563501f65f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d45986f9907903c6ccdf4d7b1c6bfe5d22eee78
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="content-queries-data-mining"></a>Consultas de contenido (minería de datos)
  Una consulta de contenido es una manera de extraer información sobre las estadísticas internas y la estructura del modelo de minería de datos. A veces, una consulta de contenido puede proporcionar detalles que no están disponibles con facilidad en el visor. También puede usar los resultados de una consulta de contenido para extraer información mediante programación para otros usos.  
  
 En esta sección se proporciona información general sobre los tipos de información que se pueden recuperar usando una consulta de contenido, así como la sintaxis DMX general para este tipo de consultas.  
  
 [Consultas básicas de contenido](#bkmk_ContentQuery)  
  
-   [Consultas en los datos de casos y de estructura](#bkmk_Structure)  
  
-   [Consultas en los patrones de modelo](#bkmk_Patterns)  
  
 [Ejemplos](#bkmk_Examples)  
  
-   [Consulta de contenido en un modelo de asociación](#bkmk_Assoc)  
  
-   [Consulta de contenido en un modelo de árboles de decisión](#bkmk_DecTree)  
  
 [Trabajar con los resultados de la consulta](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> Consultas básicas de contenido  
 Puede crear consultas de contenido mediante el Generador de consultas de predicción, use las plantillas de consulta de contenido DMX incluidas en SQL Server Management Studio, o escribir consultas directamente en DMX. A diferencia de las consultas de predicción, no es necesario combinar datos externos, por lo que las consultas de contenido son fáciles de crear.  
  
 Esta sección proporciona información general sobre los tipos de consultas de contenido que puede crear.  
  
-   Las consultas en los datos de casos o de estructura de minería de datos permiten ver los datos detallados que se utilizaron para entrenar.  
  
-   Las consultas en el modelo pueden devolver patrones, listas de atributos, fórmulas, etc.  
  
###  <a name="bkmk_Structure"></a> Consultas en los datos de casos y de estructura  
 DMX admite consultas en los datos almacenados en caché que se usan para compilar estructuras y modelos de minería de datos. De forma predeterminada, esta caché se crea al definir la estructura de minería de datos, y se rellena al procesar la estructura o el modelo.  
  
> [!WARNING]  
>  No debe borrar ni eliminar esta caché si desea separar los datos en conjuntos de entrenamiento y de prueba. Si se borra, no podrá consultar los datos de los casos.  
  
 En los siguientes ejemplos se muestran los patrones comunes para crear consultas en los datos de los casos, o consultas en los datos de la minería de datos:  
  
 **Obtener todos los casos de un modelo**  
 `SELECT FROM <model>.CASES`  
  
 Use esta instrucción para recuperar las columnas especificadas de los datos de los casos usados para compilar un modelo. Debe tener permisos de obtención de detalles en el modelo para ejecutar esta consulta.  
  
 **Ver todos los datos incluidos en la estructura**  
 `SELECT FROM <structure>.CASES`  
  
 Use esta instrucción para ver todos los datos existentes en la estructura, incluso las columnas que no están incluidas en un modelo de minería de datos determinado. Debe tener permisos de obtención de detalles en el modelo, así como en la estructura, para recuperar datos de la estructura de minería de datos.  
  
 **Obtener un intervalo de valores**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 Use esta instrucción para buscar el valor mínimo, el valor máximo y la media de una columna continua, o de los cubos de una columna de datos discretos.  
  
 **Obtener valores distintos**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 Use esta instrucción para recuperar todos los valores de una columna discreta.  No use esta instrucción para las columnas DISCRETIZED; use las funciones **RangeMin** y **RangeMax** en su lugar.  
  
 **Buscar los casos que se usaron para el entrenamiento de un modelo o una estructura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 Use esta instrucción para obtener el conjunto completo de datos empleado en el entrenamiento de un modelo.  
  
 **Buscar los casos que se usan para probar un modelo o una estructura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 Use esta instrucción para obtener los datos que se han reservado para la prueba de modelos de minería de datos relacionados con una estructura específica.  
  
 **Obtención de detalles de un patrón de modelo concreto en los datos de casos subyacentes**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 Use esta instrucción para recuperar datos detallados de los casos de un modelo entrenado. Debe especificar un nodo concreto: por ejemplo, debe conocer el identificador de nodo del clúster, la rama específica del árbol de decisión, etc. Además, debe tener permisos de obtención de detalles en el modelo para ejecutar esta consulta.  
  
###  <a name="bkmk_Patterns"></a> Consultas en los patrones, estadísticas y atributos del modelo  
 El contenido de un modelo de minería de datos es útil para muchos propósitos. Con una consulta de contenido del modelo, puede:  
  
-   Extraer fórmulas o probabilidades para realizar sus propios cálculos.  
  
-   Para un modelo de asociación, recuperar las reglas que se utilizan para generar una predicción.  
  
-   Recuperar las descripciones de reglas concretas para poder usarlas en una aplicación personalizada.  
  
-   Ver las medias móviles detectadas por un modelo de serie temporal.  
  
-   Obtener la fórmula de regresión de algún segmento de la línea de tendencia.  
  
-   Recuperar la información procesable sobre los clientes identificados como miembros de un clúster concreto.  
  
 En los siguientes ejemplos se muestran algunos de los modelos comunes para crear consultas en el contenido del modelo:  
  
 **Obtener patrones del modelo**  
 `SELECT FROM <model>.CONTENT`  
  
 Use esta instrucción para recuperar información detallada sobre nodos específicos del modelo. Dependiendo del tipo de algoritmo, el nodo puede contener reglas y fórmulas, estadísticas de compatibilidad y varianza, etc.  
  
 **Recuperar los atributos usados en un modelo entrenado**  
 `CALL System.GetModelAttributes(<model>)`  
  
 Use este procedimiento almacenado para recuperar la lista de atributos usados por un modelo. Esta información es útil para determinar los atributos que se eliminaron como resultado de la selección de características, por ejemplo.  
  
 **Recuperar el contenido almacenado en una dimensión de minería de datos**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 Use esta instrucción para recuperar los datos de una dimensión de minería de datos.  
  
 Este tipo de consulta es principalmente para uso interno. Sin embargo, no todos los algoritmos son compatibles con esta funcionalidad. Una marca indica la compatibilidad en el conjunto de filas de esquema MINING_SERVICES.  
  
 Si desarrolla su propio algoritmo de complemento, podría usar esta instrucción para comprobar el contenido del modelo para las pruebas.  
  
 **Obtener la representación PMML de un modelo**  
 `SELECT * FROM <model>.PMML`  
  
 Obtiene un documento XML que representa el modelo en formato PMML. No se admiten todos los tipos de modelos.  
  
##  <a name="bkmk_Examples"></a> Ejemplos  
 Aunque algún contenido del modelo es estándar en todos los algoritmos, algunas partes del contenido varían en gran medida dependiendo del algoritmo que se usa para compilar el modelo. Por consiguiente, al crear una consulta de contenido, debe comprender qué información del modelo resulta más útil para su modelo específico.  
  
 En esta sección se proporcionan algunos ejemplos para mostrar cómo la elección del algoritmo afecta al tipo de información que se almacena en el modelo. Para más información sobre el contenido del modelo de minería de datos y el contenido específico de cada tipo de modelo, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Assoc"></a> Ejemplo 1: consulta de contenido en un modelo de asociación  
 La instrucción `SELECT FROM <model>.CONTENT`devuelve diferentes tipos de información, según el tipo de modelo que esté consultando. Para un modelo de asociación, una información clave es el *tipo de nodo*. Los nodos son como contenedores de información en el contenido del modelo. En un modelo de asociación, los nodos que representan reglas tienen un valor NODE_TYPE de 8, mientras que los nodos que representan conjuntos de elementos tienen un valor NODE_TYPE de 7.  
  
 Así, la consulta siguiente devuelve los 10 mejores conjuntos de elementos, clasificados según el soporte (la ordenación predeterminada).  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 La consulta siguiente se basa en esta información. La consulta devuelve tres columnas: el identificador del nodo, la regla completa y el producto situado en el lado derecho del conjunto de elementos; es decir, el producto que se prevé que estará asociado a otros productos como parte de un conjunto de elementos.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 La palabra clave FLATTENED indica que el conjunto de filas anidado se debe convertir en una tabla plana. El atributo que representa el producto situado en el lado derecho de la regla se encuentra dentro de la tabla NODE_DISTRIBUTION; por consiguiente, solo recuperamos la fila que contiene un nombre de atributo, agregando el requisito de que la longitud sea mayor que 2.  
  
 Se utiliza una función de cadena sencilla para quitar el nombre del modelo de la tercera columna. (Normalmente, el nombre del modelo se antepone a los valores de las columnas anidadas).  
  
 La cláusula WHERE especifica que el valor de NODE_TYPE debe ser 8 para recuperar solo reglas.  
  
 Para obtener más ejemplos, vea [Ejemplos de consultas del modelo de asociación](../../analysis-services/data-mining/association-model-query-examples.md).  
  
###  <a name="bkmk_DecTree"></a> Ejemplo 2: consulta de contenido en un modelo de árboles de decisión  
 Un modelo del árbol de decisión se puede utilizar para la predicción así como para la clasificación.  En este ejemplo se supone que está utilizando el modelo para predecir un resultado, pero también desea descubrir qué factores o reglas se pueden utilizar para clasificar el resultado.  
  
 En un modelo de árbol de decisión, los nodos se utilizan para representar árboles y nodos de hoja. El título de cada nodo contiene la descripción de la ruta de acceso al resultado. Por consiguiente, para realizar el seguimiento de la ruta de acceso de cualquier resultado determinado, debe identificar el nodo que lo contiene y obtener los detalles de ese nodo.  
  
 En la consulta de predicción, agregue la función de predicción [PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md) para obtener el identificador del nodo relacionado, como se muestra en el siguiente ejemplo:  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 Una vez obtenido el identificador del nodo que contiene el resultado, puede recuperar la regla o la ruta de acceso que explica la predicción creando una consulta de contenido que incluya NODE_CAPTION como la siguiente:  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 Para obtener más ejemplos, vea [Ejemplos de consultas de modelos de árboles de decisión](../../analysis-services/data-mining/decision-trees-model-query-examples.md).  
  
##  <a name="bkmk_Results"></a> Trabajar con los resultados de la consulta  
 Como demuestran los ejemplos, las consultas de contenido devuelven principalmente conjuntos de filas tabulares, pero también pueden incluir información de columnas anidadas. Es posible simplificar el conjunto de filas que se devuelven, pero esto puede dificultar el trabajo con los resultados. El contenido del nodo NODE_DISTRIBUTION en concreto está anidado, pero contiene información muy interesante sobre el modelo.  
  
 Para obtener más información sobre cómo trabajar con conjuntos de filas jerárquicos, vea la especificación OLEDB en MSDN.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la instrucción Select de DMX](../../dmx/understanding-the-dmx-select-statement.md)   
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
