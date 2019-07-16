---
title: MODIFICAR LA ESTRUCTURA DE MINERÍA DE DATOS (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 487fb5c04d623f2a4ef408cf35784dd57b067f4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913840"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuevo modelo de minería de datos basado en una estructura de minería de datos existente.  Cuando se usa el **ALTER MINING STRUCTURE** instrucción para crear un nuevo modelo de minería de datos, la estructura ya debe existir. En cambio, cuando se usa la instrucción, [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), crear un modelo y generar automáticamente su estructura de minería de datos subyacente al mismo tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>Argumentos  
 *estructura*  
 Nombre de la estructura de minería de datos a la que se agregará el modelo de minería de datos.  
  
 *model*  
 Nombre único del modelo de minería de datos.  
  
 *lista de definiciones de columna*  
 Lista delimitada por comas de definiciones de columna.  
  
 *lista de definiciones de columna anidada*  
 Lista delimitada por comas de columnas de una tabla anidada, si procede.  
  
 *criterios de filtro anidado*  
 Expresión de filtro que se aplica a las columnas de una tabla anidada.  
  
 *algorithm*  
 Nombre de un algoritmo de minería de datos definido por el proveedor.  
  
> [!NOTE]  
>  Se puede recuperar una lista de los algoritmos admitidos por el proveedor actual mediante [filas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Para ver los algoritmos admitidos en la instancia actual de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md).  
  
 *lista de parámetros*  
 Opcional. Lista delimitada por comas de parámetros definidos por el proveedor para el algoritmo.  
  
 *criterios de filtro*  
 Expresión de filtro que se aplica a las columnas de la tabla de casos.  
  
## <a name="remarks"></a>Comentarios  
 Si la estructura de minería de datos contiene claves compuestas, el modelo de minería debe incluir todas las columnas de clave que están definidas en la estructura.  
  
 Si el modelo no requiere una columna de predicción, como ocurre con los modelos que se generan mediante los algoritmos de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)] y de agrupación en clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)], no es necesario incluir una definición de columna en la instrucción. Todos los atributos del modelo resultante se tratarán como entradas.  
  
 En el **WITH** cláusula que se aplica a la tabla de casos, puede especificar opciones de filtrado y de obtención de detalles:  
  
-   Agregar el **filtro** palabra clave y una condición de filtro. El filtro se aplica a los casos del modelo de minería de datos.  
  
-   Agregar el **obtención de detalles** palabra clave para permitir que los usuarios del modelo de minería de datos explorar en profundidad los resultados del modelo para los datos del caso. En las extensiones de minería de datos (DMX), obtención de detalles puede habilitarse únicamente cuando se crea el modelo.  
  
 Para usar mayúsculas filtrado y la obtención de detalles, combina las palabras clave en una sola **WITH** cláusula utilizando la sintaxis que se muestra en el ejemplo siguiente:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Lista de definiciones de columna  
 Para definir la estructura de un modelo, especifique una lista de definiciones de columna que incluya la información siguiente para cada columna:  
  
-   Nombre (obligatorio)  
  
-   Alias (opcional)  
  
-   Marcas de modelado  
  
-   Solicitud de predicción, que indica al algoritmo si la columna contiene un valor de predicción, indicado por el **PREDICT** o **PREDICT_ONLY** cláusula  
  
 Use la siguiente sintaxis en la lista de definiciones de columna para definir una sola columna:  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Nombre y alias de la columna  
 El nombre de columna que se utiliza en la lista de definiciones de columna debe ser el nombre de la columna tal como se utiliza en la estructura de minería de datos. Sin embargo, también se puede definir un alias para representar la columna de estructura en el modelo de minería de datos. Asimismo, se pueden crear varias definiciones de columna para la misma columna de estructura y asignar a cada copia de la columna un alias y uso de predicción diferentes. De forma predeterminada, se utiliza el nombre de la columna de estructura si no se define un alias. Para obtener más información, consulte [crear un Alias para una columna de modelo](../analysis-services/data-mining/create-an-alias-for-a-model-column.md).  
  
 Para las columnas de tabla anidada, especifique el nombre de la tabla anidada, especifique el tipo de datos como **tabla**y, a continuación, proporcione la lista de las columnas anidadas para incluir en el modelo, encerrada entre paréntesis.  
  
 Para definir una expresión de filtro que se aplique a la tabla anidada, adjunte una expresión de criterios de filtro después de la definición de columna de la tabla anidada.  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite las marcas de modelado siguientes en las columnas del modelo de minería de datos:  
  
> [!NOTE]  
>  La marca de modelado NOT_NULL se aplica a la columna de estructura de minería de datos. Para obtener más información, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Término|Definición|  
|**REGRESSOR**|Indica que el algoritmo puede usar la columna especificada en la fórmula de regresión de algoritmos de regresión.|  
|**MODEL_EXISTENCE_ONLY**|Indica que los valores de la columna de atributos no son tan importantes como la presencia del atributo.|  
  
 Puede definir varias marcas de modelado para una columna. Para obtener más información sobre cómo usar marcas de modelado, vea [marcas de modelado &#40;DMX&#41;](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Cláusula de predicción  
 La cláusula de predicción describe cómo se usa la columna de predicción. En la tabla siguiente se enumeran las cláusulas posibles.  
  
|||  
|-|-|  
|**PREDICT**|Esta columna puede predecirla el modelo y sus valores se pueden usar como entrada para predecir el valor de otras columnas de predicción.|  
|**PREDICT_ONLY**|Esta columna puede predecirla el modelo, pero sus valores no se pueden utilizar en escenarios de entrada para predecir el valor de otras columnas de predicción.|  
  
## <a name="filter-criteria-expressions"></a>Expresiones de criterios de filtro  
 Puede definir un filtro que restrinja los casos que se utilizan en el modelo de minería de datos. El filtro se puede aplicar a las columnas de la tabla de casos, a las filas de la tabla anidada, o a ambas.  
  
 Las expresiones de criterios de filtro son predicados DMX simplificados, similares a una cláusula WHERE. Las expresiones de filtro se reducen a fórmulas que utilizan operadores matemáticos básicos, escalares y nombres de columna. La excepción la constituye el operador EXISTS; se evalúa como TRUE si la subconsulta devuelve al menos una fila. Los predicados se pueden combinar mediante el uso de los operadores lógicos comunes: AND, OR y no.  
  
 Para obtener más información acerca de los filtros utilizados con los modelos de minería de datos, vea [filtros para modelos de minería de datos de &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Las columnas de un filtro deben ser columnas de estructura de minería de datos. No se puede crear un filtro para una columna del modelo ni para una columna con alias.  
  
 Para obtener más información sobre la sintaxis y los operadores DMX, vea [columnas del modelo de minería de datos](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="parameter-definition-list"></a>Lista de definiciones de parámetros  
 Para ajustar el rendimiento y la funcionalidad de un modelo, se pueden agregar parámetros del algoritmo a la lista de parámetros. Los parámetros que se pueden utilizar dependen del algoritmo que se especifique en la cláusula USING. Para obtener una lista de parámetros que están asociados con cada algoritmo, vea [algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 La sintaxis de la lista de parámetros es:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Ejemplo 1: Agregar un modelo a una estructura  
 En el ejemplo siguiente se agrega un modelo de minería de datos Bayes Naive a la **New Mailing** estructura de minería de datos y los límites indica el número máximo de atributo a 50.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Ejemplo 2: Agregar un modelo filtrado a una estructura  
 En el ejemplo siguiente se agrega un modelo de minería de datos, `Naive Bayes Women`, a la **New Mailing** estructura de minería de datos. El nuevo modelo tiene la misma estructura básica que el modelo de minería de datos que se agregó en el ejemplo 1; sin embargo, este modelo restringe los casos de la estructura de minería de datos a las clientas con una edad superior a 50 años.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Ejemplo 3: Agregar un modelo filtrado a una estructura con una tabla anidada  
 En el ejemplo siguiente se agrega un modelo de minería de datos a una versión modificada de la estructura de minería de datos Market Basket. La estructura de minería de datos usada en el ejemplo se ha modificado para agregar un **región** columna, que contiene los atributos de la región del cliente, y un **Income Group** columna, que clasifica los ingresos del cliente mediante el uso de los valores **alta**, **moderado**, o **bajo**.  
  
 La estructura de minería de datos también incluye una tabla anidada que contiene los artículos comprados por el cliente.  
  
 Dado que la estructura de minería de datos contiene una tabla anidada, es posible definir un filtro para la tabla de casos, la tabla anidada, o ambas. En este ejemplo se combinan un filtro de casos y uno de filas anidadas para restringir los casos a los clientes europeos adinerados que compraron uno de los modelos con neumáticos de carretera.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
