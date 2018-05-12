---
title: 'Tablas anidadas (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35444ae17ac4a11bd0321e70631f45d84273e0af
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="nested-tables-analysis-services---data-mining"></a>Tablas anidadas (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los datos se deben incluir en un algoritmo de minería de datos como una serie de casos contenidos dentro de una tabla de casos. Sin embargo, no todos los casos pueden describirse mediante una sola fila de datos. Por ejemplo, un caso puede derivarse de dos tablas: una que contenga la información del cliente y otra que contenga las compras de ese cliente. Un solo cliente de la tabla de información de clientes podría tener varios elementos en la tabla de compras del cliente, lo que dificulta describir los datos mediante una sola fila. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Proporciona un método único para tratar estos casos, mediante *tablas anidadas*. El concepto de una tabla anidada se muestra en la siguiente ilustración.  
  
 ![Dos tablas se combinan mediante una tabla anidada](../../analysis-services/data-mining/media/nested-tables.gif "dos tablas se combinan mediante una tabla anidada")  
  
 En este diagrama, la primera tabla, que es la tabla primaria, contiene información sobre los clientes y asocia cada cliente con un único identificador. La segunda tabla, la tabla secundaria, contiene las compras de cada cliente. Las compras de la tabla secundaria se relacionan con la tabla primaria mediante el identificador único, la columna **CustomerKey** . La tercera tabla del diagrama muestra cómo se combinan ambas tablas.  
  
 Una tabla anidada se representa en la tabla de casos como una columna especial que tiene un tipo de datos **TABLE**. En las filas específicas de caso, esta clase de columna contiene filas seleccionadas de la tabla secundaria que forman parte de la tabla primaria.  
  
 Los datos de una tabla anidada se pueden utilizar para la predicción, como entrada o para ambos. Por ejemplo, podría tener dos columnas de tabla anidada en un modelo: una podría contener una lista de los productos que un cliente ha comprado, mientras que la otra podría contener información sobre las aficiones e intereses del cliente, posiblemente obtenidas en un estudio. Podría utilizar las aficiones e intereses del cliente como entrada para analizar el comportamiento de compra y predecir las compras probables.  
  
## <a name="joining-case-tables-and-nested-tables"></a>Combinar tablas de casos y tablas anidadas  
 A fin de crear una tabla anidada, las dos tablas de origen deben contener una relación definida de forma que los elementos de una tabla puedan relacionarse con los de la otra. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se puede definir esta relación en la vista del origen de datos.  
  
> [!NOTE]  
>  El campo **CustomerKey** es la clave relacional usada para vincular la tabla de casos y la tabla anidada dentro de la definición de vista del origen de datos, así como para establecer la relación de las columnas dentro de la estructura de minería de datos. Sin embargo, normalmente no se debe usar esta clave relacional en los modelos de minería de datos generados en dicha estructura. Por lo general, es preferible omitir la columna de clave relacional del modelo de minería de datos si solo sirve para combinar las tablas y no proporciona información que merezca la pena analizar.  
  
 Puede crear tablas anidadas mediante programación usando Extensiones de minería de datos (DMX) u Objetos de administración de análisis (AMO), o puede utilizar el Asistente para minería de datos y el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="using-nested-table-columns-in-a-mining-model"></a>Usar columnas de tabla anidada en un modelo de minería de datos  
 En la tabla de casos, la clave es a menudo un identificador de cliente, un nombre de producto o una fecha dentro una serie; es decir, datos que identifican una fila en la tabla de forma inequívoca. . Sin embargo, en las tablas anidadas, normalmente la clave no es la clave relacional (o clave externa), sino la columna que representa el atributo que se está modelando.  
  
 Por ejemplo, si la tabla de casos contiene pedidos y la tabla anidada contiene los artículos de cada uno de dichos pedidos, le interesaría modelar la relación entre los artículos almacenados en la tabla anidada y los pedidos, que se almacenan en la tabla de casos. Por lo tanto, aunque la tabla anidada **Items** se combina con la tabla de casos **Orders** mediante la clave relacional **OrderID**, no se debe usar **OrderID** como clave de la tabla anidada. En su lugar, se debe seleccionar la columna **Items** , ya que dicha columna contiene los datos que se desea modelar. En la mayoría de los casos, se puede pasar por alto **OrderID** sin ningún problema en el modelo de minería de datos, ya que la relación entre la tabla de casos y la tabla anidada ya ha sido establecida por la definición de vista del origen de datos.  
  
 Cuando elija la columna que se va a usar como clave de la tabla anidada, debe asegurarse de que los valores de dicha columna sean únicos para cada caso. Por ejemplo, si la tabla de casos representa clientes y la tabla anidada representa los artículos adquiridos por cada cliente, debe asegurarse de que ningún artículo aparezca varias veces por cliente. Si un cliente ha adquirido el mismo artículos varias veces, debe crear una vista diferente con una columna que agregue el número de compras para cada producto único.  
  
 La decisión de cómo administrar los valores duplicados en una tabla anidada dependerá del modelo de minería de datos que esté creando y del problema empresarial que esté intentando resolver. En algunos escenarios, es posible que no le interese el número de veces que un cliente ha adquirido un determinado producto sino que solo desee comprobar la existencia de al menos una compra. En otros escenarios, es posible que la cantidad y la secuencia de compras sean de gran importancia.  
  
 Si el orden de los artículos es importante, puede que necesite una columna adicional que indique la secuencia. Cuando use el algoritmo de clústeres de secuencia para crear un modelo, deberá elegir una columna *Key Sequence* adicional para representar el orden de los artículos. La columna Key Sequence es una clase especial de clave anidada que solo se usa en modelos de agrupación en clústeres de secuencia, y requiere un tipo de datos numérico único. Por ejemplo, los enteros y las fechas se pueden usar como columna Key Sequence, pero todos los valores de secuencia deben ser únicos. Además de la columna Key Sequence, un modelo de agrupación en clústeres de secuencia también incluye una clave de tabla anidada que representa el atributo que se está modelando, como los productos que se han adquirido.  
  
### <a name="using-non-key-nested-columns-from-a-nested-table"></a>Usar columnas anidadas sin clave desde una tabla anidada  
 Una vez definida la combinación entre la tabla de casos y la tabla anidada, y después de elegir la columna que contiene atributos interesantes y únicos que se pueden usar como clave de la tabla anidada, puede incluir otras columnas de la tabla anidada para usarlas como entrada para el modelo. Todas las columnas de la tabla anidada se pueden usar como entrada, como predicción y entrada, o solo como predicción.  
  
 Por ejemplo, si la tabla anidada contiene las columnas **Product**, **ProductQuantity**y **ProductPrice**, se puede elegir **Product** como clave de la tabla anidada, pero se ha de agregar **ProductQuantity** a la estructura de minería de datos para usarla como entrada.  
  
## <a name="filtering-nested-table-data"></a>Filtrar datos de tablas anidadas  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]se pueden crear filtros para los datos que se usan en la comprobación o el entrenamiento de un modelo de minería de datos. Puede utilizarse un filtro que afecte a la composición del modelo, o para probar el modelo en un subconjunto de casos. Los filtros también se pueden aplicar a las tablas anidadas. Sin embargo, existen limitaciones en cuanto a la sintaxis que se puede usar con dichas tablas.  
  
 A menudo se aplica un filtro a una tabla anidada para comprobar si un atributo existe o no existe. Por ejemplo, se puede aplicar un filtro que restrinja los casos usados en el modelo a solo aquellos que tengan un valor especificado en la tabla anidada. O bien, se pueden restringir los casos utilizados en el modelo a los clientes que no han adquirido un artículo determinado.  
  
 Al crear filtros en una tabla anidada, también se pueden usar operadores, como mayor que o menor que. Por ejemplo, puede restringir los casos usados en el modelo a los clientes que hayan comprado al menos n unidades del producto en cuestión. La posibilidad de filtrar atributos de tabla anidada proporciona una gran flexibilidad a la hora de personalizar los modelos.  
  
 Para obtener más información sobre cómo crear y usar filtros de modelos, vea [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estructuras de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
