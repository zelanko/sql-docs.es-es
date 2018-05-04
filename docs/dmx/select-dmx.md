---
title: SELECT (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SELECT
dev_langs:
- DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- TOP clause, SELECT
- FLATTENED option
- predictions [DMX]
- ORDER BY clause [DMX]
- SELECT statement [DMX]
- mining models [Analysis Services], browsing
- statements [DMX], SELECT statement
- WHERE clause, DMX
ms.assetid: 32d9e8fd-796b-4e1c-ae59-73cd6f645485
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c22aff659dc4de5bd5a16cf927aaf391fa856af4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El **seleccione** instrucción de extensiones de minería de datos (DMX) se utiliza para las siguientes tareas en minería de datos:  
  
-   Examinar el contenido de un modelo de minería de datos existente  
  
-   Crear predicciones a partir de un modelo de minería de datos existente  
  
-   Crear una copia de un modelo de minería de datos existente  
  
-   Examinar la estructura de minería de datos  
  
 Aunque la sintaxis completa de esta instrucción es compleja, las cláusulas principales utilizadas para examinar un modelo y su estructura subyacente se pueden resumir del modo siguiente:  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 Algunos clientes de minería de datos no pueden aceptar conjuntos de resultados en formato jerárquico de un proveedor de minería de datos. El cliente podría carecer de la capacidad de tratar una jerarquía o podría tener que almacenar los resultados en una sola tabla no normalizada. Para convertir los datos de tablas anidadas en tablas sin información de estructura jerárquica, es necesario solicitar que los resultados de consulta no tengan este tipo de información.  
  
 Para simplificar los resultados de consulta, use la **seleccione** sintaxis con el **FLATTENED** opción, tal como se muestra en el ejemplo siguiente:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>Parte superior \<n > y ORDER BY  
 Puede ordenar los resultados de una consulta mediante el uso de una expresión y, a continuación, se puede devolver un subconjunto de los resultados mediante una combinación de la **ORDER BY** y **arriba** cláusulas. Esto resulta útil en un escenario como el correo directo, en el que solo se desea enviar resultados a los destinatarios que tienen más probabilidad de responder. Puede ordenar los resultados de un consulta de predicción de correo por la probabilidad de predicción de destino y, a continuación, devolver sólo la parte superior \<n > resultados.  
  
## <a name="select-list"></a>Lista de selección  
 El  *\<lista de selección >* pueden incluir referencias a columna escalares, funciones de predicción y expresiones. Las opciones que estén disponibles dependen del algoritmo y de los contextos siguientes:  
  
-   Si está consultando una estructura de minería de datos o un modelo de minería de datos  
  
-   Si está consultando contenido o casos  
  
-   Si los datos de origen son una tabla relacional o un cubo  
  
-   Si está realizando predicciones  
  
 En muchos casos, puede utilizar alias o crear expresiones simples basadas en los elementos de la lista de selección. En el ejemplo siguiente se muestra una expresión simple en columnas de modelo:  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 En el ejemplo siguiente se crea un alias para una columna que contiene los resultados de una función de predicción:  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 Puede limitar los casos que son devueltos por la consulta mediante el uso de un **donde** cláusula. El **donde** cláusula especifica hace referencia a esa columna en la **donde** expresión debe tener la misma semántica que las referencias de columna en la  *\<lista de selección >* de la **seleccione** instrucción y solo pueden devolver una expresión booleana. La sintaxis para la **donde** cláusula es como se indica a continuación.  
  
```  
WHERE < condition expression >  
```  
  
 La lista de selección y **donde** cláusula de una **seleccione** instrucción debe seguir las reglas siguientes:  
  
-   La lista de selección debe contener una expresión que no devuelva un resultado booleano. Puede modificar la expresión, pero debe devolver un resultado no booleano.  
  
-   El **donde** cláusula debe contener una expresión que devuelve un resultado booleano. Puede modificar la cláusula, pero debe devolver un resultado booleano.  
  
## <a name="predictions"></a>Predicciones  
 Puede usar dos tipos de sintaxis para crear predicciones:  
  
-   [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;modelo&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 El primer tipo de predicción le permite crear predicciones complejas en tiempo real o como lote.  
  
 El segundo tipo de predicción crea una combinación de predicción vacía en una columna de predicción de un modelo de minería de datos y devuelve el estado más probable de la columna. Los resultados de esta consulta están basados completamente en el contenido del modelo de minería de datos.  
  
 Puede insertar una instrucción select en la consulta de origen de una instrucción SELECT FROM PREDICTION JOIN mediante la siguiente sintaxis.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Para obtener más información acerca de cómo crear consultas de predicción, vea [estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Sintaxis de cláusulas  
 Debido a la complejidad de la exploración con el **seleccione** instrucción, elementos de sintaxis detallada y los argumentos se describen con cláusulas. Para obtener más información acerca de cada cláusula, haga clic en un tema de la siguiente lista:  
  
 [SELECT DISTINCT FROM &#60;modelo &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;modelo&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60;estructura&#62;. CASOS](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)  
  
  
