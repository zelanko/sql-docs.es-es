---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8bf766c6f0a7fd757b280b0f950a43cfdc025929
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928423"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La instrucción **Select** de extensiones de minería de datos (DMX) se utiliza para las siguientes tareas en la minería de datos:  
  
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
  
 Para aplanar los resultados de la consulta, use la sintaxis **Select** con la opción **Flatten** , tal como se muestra en el ejemplo siguiente:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n> y order by  
 Puede ordenar los resultados de una consulta mediante una expresión y, a continuación, devolver un subconjunto de los resultados usando una combinación de las cláusulas **order by** y **Top** . Esto resulta útil en un escenario como el correo directo, en el que solo se desea enviar resultados a los destinatarios que tienen más probabilidad de responder. Puede ordenar los resultados de una consulta de predicción de correo de destino por la probabilidad de predicción y, a continuación, \<devolver solo los n primeros> resultados.  
  
## <a name="select-list"></a>Lista de selección  
 La * \<lista de selección>* puede incluir referencias de columnas escalares, funciones de predicción y expresiones. Las opciones que estén disponibles dependen del algoritmo y de los contextos siguientes:  
  
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
 Puede limitar los casos devueltos por la consulta mediante el uso de una cláusula **Where** . La cláusula **Where** especifica que las referencias de columna en la expresión **Where** deben tener la misma semántica que las referencias de columna en la * \<lista de selección>* de la instrucción **Select** , y solo pueden devolver una expresión booleana. La sintaxis de la cláusula **Where** es la siguiente:  
  
```  
WHERE < condition expression >  
```  
  
 La lista de selección y la cláusula **Where** de una instrucción **Select** deben seguir las reglas siguientes:  
  
-   La lista de selección debe contener una expresión que no devuelva un resultado booleano. Puede modificar la expresión, pero debe devolver un resultado no booleano.  
  
-   La cláusula **Where** debe contener una expresión que devuelva un resultado booleano. Puede modificar la cláusula, pero debe devolver un resultado booleano.  
  
## <a name="predictions"></a>Predicciones  
 Puede usar dos tipos de sintaxis para crear predicciones:  
  
-   [Seleccione entre &#60;modelo&#62; combinación de predicción &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;Model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 El primer tipo de predicción le permite crear predicciones complejas en tiempo real o como lote.  
  
 El segundo tipo de predicción crea una combinación de predicción vacía en una columna de predicción de un modelo de minería de datos y devuelve el estado más probable de la columna. Los resultados de esta consulta están basados completamente en el contenido del modelo de minería de datos.  
  
 Puede insertar una instrucción SELECT en la consulta de origen de una instrucción SELECT FROM PREDICT JOIN mediante la sintaxis siguiente.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Para obtener más información sobre cómo crear consultas de predicción, vea [estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Sintaxis de cláusulas  
 Debido a la complejidad de la exploración con la instrucción **Select** , los elementos y argumentos de sintaxis detallados se describen mediante la cláusula. Para obtener más información acerca de cada cláusula, haga clic en un tema de la siguiente lista:  
  
 [Seleccione DISTINCt FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [Seleccione entre &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [Seleccione entre &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [Seleccione entre &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [Seleccione entre &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [Seleccione entre &#60;modelo&#62; combinación de predicción &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;Model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [Seleccione de &#60;estructura&#62;. VECES](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Consulte también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)  
  
  
