---
title: Análisis de la cesta de compras (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shopping basket analysis
- mining model, association
- Table Analysis tools
- association [data mining]
- market basket analysis
ms.assetid: ba40cf43-f286-49ad-8316-70f5b11f1dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dadc054a3f9927c09e9e236044dd5ddee7f3a9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068681"
---
# <a name="shopping-basket-analysis-table-analysistools-for-excel"></a>Análisis de la cesta de compras (Herramientas de análisis de tabla para Excel)
  ![Herramienta cesta](media/tat-shopbskt.gif "herramienta cesta de la compra")  
  
 El **análisis de cesta de la compra** herramienta le ayuda a encontrar `associations` en los datos. Una asociación podría indicarle cuáles son los artículos que se suelen comprar al mismo tiempo. En la minería de datos, esta técnica es un método muy conocido que se conoce como *análisis de cesta*, que se usa para analizar los hábitos de compra de los clientes de grandes conjuntos de datos. Los vendedores pueden usar la información para realizar recomendaciones a los clientes sobre productos relacionados y promocionar estos colocándolos muy cerca unos de otros en páginas Web, catálogos o en la misma estantería.  
  
 Para usar el análisis de la cesta de compras, los artículos que desea analizar deben estar relacionados por un identificador de transacción. Por ejemplo, si está analizando todos los pedidos recibidos a través de un sitio Web, cada uno de ellos tendrá un identificador de pedido o de transacción que estará relacionado con uno o más de los productos adquiridos.  
  
 Cuando el asistente termina de analizar los datos, se crean dos nuevas hojas de cálculo, **Shopping Basket Item Groups** y **Shopping Basket Rules**.  
  
 El **Shopping Basket Item Groups** hoja de cálculo contiene una lista de los elementos que suelen aparecer juntos en las transacciones. Estas agrupaciones comunes se denominan *conjuntos de elementos*. La hoja de cálculo también contiene estadísticas, como *admite* y *elevación*, que le ayudarán a entender la importancia del conjunto de elementos. Si la información sobre el precio está disponible, la hoja de cálculo también crea una suma del valor de todos los elementos relacionados, con objeto de proporcionar una indicación del valor total de las transacciones.  
  
 Puede filtrar y ordenar las columnas del informe. Por ejemplo, es posible que desee ver solo los conjuntos de elementos con 2 o más productos, u ordenarlos por **Average Basket Value**.  
  
 El **Shopping Basket Rules** hoja de cálculo utiliza las estadísticas derivadas del análisis para crear reglas sobre cómo se relacionan los elementos. Por ejemplo, una regla podría ser que si los clientes compran el producto A, están muy probables que compren el producto B. Las reglas se pueden usar para crear recomendaciones. Cada regla dispone de estadísticas que le permiten evaluar su solidez potencial, de forma que pueda realizar una recomendación solo si la regla supera un cierto umbral de probabilidad.  
  
## <a name="using-the-shopping-basket-analysis-tool"></a>Usar la herramienta Análisis de la cesta de compras  
  
1.  Abra una tabla de Excel que contenga datos apropiados. En el libro de ejemplo, haga clic en la hoja de cálculo Associate.  
  
2.  Haga clic en **análisis de cesta**.  
  
3.  En el **análisis de cesta de la compra** cuadro de diálogo, elija la columna que contiene el identificador de transacción y, a continuación, elija la columna que contiene los elementos o los productos que desea analizar.  
  
4.  Si lo desea, puede agregar una columna que contenga valores de producto.  
  
5.  Haga clic en**avanzadas**para abrir el **configuración avanzada de los parámetros** cuadro de diálogo. Aumente el valor de **soporte mínimo** para reducir el número de productos que se agrupan como conjuntos de elementos. Aumentar la **probabilidad de regla mínima** para filtrar los conjuntos de elementos muy comunes.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el **análisis de cesta de la compra** herramienta, los datos deben almacenarse en una tabla de Excel y debe contener las columnas siguientes:  
  
-   La columna que contiene un identificador único que representa la transacción. El identificador puede ser numérico o de texto, siempre que el valor de cada fila sea único.  
  
-   La columna que contiene el elemento o el producto que se está analizando.  
  
-   Una columna numérica opcional que representa el precio o el valor de cada elemento. Esta columna se usa para agregar el valor de los conjuntos de elementos en los que se encuentra cada producto, y puede ayudarle a comprender el valor total de ciertas transacciones.  
  
## <a name="how-items-are-associated"></a>Cómo se asocian los elementos  
 Los elementos individuales que se analizan deben agruparse mediante algún identificador que represente el caso, la transacción o la ocasión. Por lo tanto, se elegirá esta columna de identificador de transacción como identificador, y no el número de identificador de cliente o el número de identificador de producto.  
  
 Cuando la herramienta examina los productos dentro de cada transacción, crea un conjunto de elementos para cada combinación de elementos que encuentra. Por ejemplo, si un cliente compró tres artículos en una única visita, hay 7 conjuntos de elementos posibles: cada producto considerado por sí solo, cada producto agrupado con otro y la combinación de los tres productos.  
  
> [!NOTE]  
>  Puede filtrar los conjuntos de elementos que contienen elementos individuales para descartarlos, pero la herramienta necesita analizarlos para generar estadísticas significativas para el conjunto de datos.  
  
 La compatibilidad de cada conjunto de elementos se calcula como el número de clientes que compran un conjunto de elementos. Siguiendo con el ejemplo planteado, si únicamente un cliente ha comprado 3 elementos, con 7 posibles conjuntos de elementos, cada uno de los 7 conjuntos de elementos tiene un valor de compatibilidad de 1. A medida que crece el número de clientes y el de combinaciones posibles, aumenta el tiempo necesario para procesar el informe. Sin embargo, algunos conjuntos de elementos pueden tener una compatibilidad muy pequeña. Por lo tanto, puede optar por reducir el tiempo empleado en generar el informe limitando el número de elementos de cada conjunto de elementos a 3 o menos. Generalmente, los conjuntos de elementos grandes tienen mucha menos compatibilidad inferior, por lo que esta reducción resulta aceptable.  
  
## <a name="specifying-minimum-support-and-rule-probability"></a>Especificar la compatibilidad mínima y la probabilidad de regla mínima  
 A medida que el conjunto de datos aumenta de tamaño, el número de posibles agrupaciones de elementos y reglas puede resultar abrumador. Sin embargo, puede controlar el número de resultados generados por la herramienta para centrarse sólo en los conjuntos de elementos y reglas más valiosos. Puede establecer estas opciones el **Shopping Basket Advanced parámetros Dialog Box**.  
  
### <a name="minimum-support"></a>Compatibilidad mínima  
 *Soporte mínimo* significa el número de transacciones que debe contener un conjunto de elementos determinado para el conjunto de elementos que se consideran significativas. Por ejemplo, puede no estar interesado en un conjunto de elementos a menos que se haya comprado en al menos 10 transacciones diferentes. Hay dos maneras de controlar el umbral de importancia del conjunto de elementos, y ambas usan el **soporte mínimo** parámetro.  
  
 **Como un valor absoluto:** Escriba un número que representa el recuento de transacciones que contienen los elementos de destino. Por ejemplo, si escribe 10, cualquier conjunto de elementos que aparezca en al menos 10 cestas de la compra estará incluido en los resultados.  
  
 **Como un porcentaje:** Escriba un número que representa un porcentaje de toda la colección de conjuntos de elementos. Por ejemplo, si especifica 10, se cuentan todos los conjuntos de elementos y el conjunto de elementos de destino debe constituir al menos el 10 por ciento del número total de conjuntos de elementos. Si tiene un conjunto de datos de gran tamaño, el uso de porcentajes en lugar de recuentos puede ayudarle a centrarse en las agrupaciones de elementos más importantes.  
  
> [!NOTE]  
>  No olvide que el número de conjuntos de elementos es distinto del número de transacciones de los datos. Cada transacción puede contener varios conjuntos de elementos; sin embargo, la mayoría de éstos se repiten varias veces en el conjunto de datos.  
  
### <a name="rule-probability-and-rule-importance"></a>Probabilidad e importancia de la regla  
 La probabilidad de una regla describe la posibilidad de que se produzca su resultado. La probabilidad de regla se calcula con la frecuencia de los conjuntos de elementos compatibles con una regla. Si un conjunto de elementos se produce con poca frecuencia, su probabilidad será baja.  
  
 Sin embargo, las reglas que tienen una probabilidad alta no son siempre útiles. Podrían indicar conjuntos de elementos que se compran con frecuencia y que, por consiguiente, no necesitan ninguna promoción adicional. La importancia está diseñada para medir la utilidad de una regla. A veces, una regla puede tener una probabilidad muy alta pero poca importancia, ya que la predicción no proporciona nueva información. Por ejemplo, si cada conjunto de elementos contiene un estado específico de un atributo, una regla que predice ese estado no será muy significativa, aunque la probabilidad sea muy alta.  
  
 Conviene que experimente con estos valores para ver los distintos resultados y determinar qué valor produce las reglas más interesantes.  
  
## <a name="understanding-the-reports"></a>Descripción de los informes  
 El **análisis de cesta de la compra** herramienta crea dos informes complementarios. El primer informe, denominado **grupos significativos de los elementos identificados durante el análisis**, proporciona una lista de todos los conjuntos de elementos que se han encontrado. Puede usar las nuevas herramientas de tabla de Microsoft Excel para ordenar, filtrar y explorar los datos.  
  
 El segundo informe, denominado **Shopping Basket Rules**, indica el tipo de inferencias se puede realizar basándose en los conjuntos de elementos enumerados en el primer informe. Mientras que la lista de conjuntos de elementos es más útil para explorar y entender los datos, la lista de reglas es más útil para realizar predicciones y recomendaciones.  
  
### <a name="shopping-basket-item-groups-report"></a>Informe Shopping Basket Item Groups  
 Este informe contiene una lista de todas las posibles combinaciones de elementos encontradas en el conjunto de datos. Por ejemplo, si los datos de transacción contienen pedidos de cada pedido el **análisis de cesta de la compra** herramienta calcula cuántas veces se ha pedido el elemento individual y, a continuación, calcula todas las combinaciones de ese elemento con otros elementos.  
  
 El informe muestra los conjuntos de elementos encontrados ordenados por la mejora respecto al modelo predictivo. La mejora respecto al modelo predictivo es una puntuación que le indica la importancia del conjunto de elementos.  
  
|Columna del informe|¿Qué indica|  
|----------------------|-----------------------|  
|Group of Items|Muestra los conjuntos de elementos, o una combinación de elementos.|  
|Group Size|Recuento del número de elementos del conjunto de elementos. Puede filtrar por este campo si desea ver solo pares de elementos, elementos individuales, etc.|  
|Soporte técnico|Recuento del número de casos en los que se produjo esta combinación. Puede ordenar por esta columna para ver los conjuntos de elementos más comunes.|  
|Average Value|Suma de los valores de los elementos de este conjunto de elementos, dividida por la compatibilidad. Puede ordenar y filtrar por esta columna para dirigirse a productos en distintos intervalos de precio.|  
|Average Basket Value|Suma de los valores de todos los elementos en los pedidos que contienen este conjunto de elementos, dividida por la compatibilidad. Esta estadística es interesante cuando va emparejada con el valor medio del conjunto de elementos.|  
|Mejora respecto al modelo predictivo|Puntuación que representa lo interesante que es este conjunto de elementos en el conjunto de datos completo. La mejora respecto al modelo predictivo se calcula obteniendo la probabilidad de que los dos elementos se produzcan juntos y, a continuación, dividiéndola por la probabilidad de que los dos elementos se produzcan de forma independiente. En consecuencia, si hay una correlación fuerte entre los elementos, la puntuación de la mejora respecto al modelo predictivo será más alta.|  
  
### <a name="shopping-basket-rules-report"></a>Informe Reglas de la cesta de compra  
 Este informe contiene un conjunto de reglas generadas a partir del análisis de los conjuntos de elementos encontrados. Por ejemplo, si los datos de la transacción revelan que los productos A y B se compran con frecuencia juntos, la herramienta Análisis de la cesta de compras creará una regla que predice A a partir de la existencia de B, o B a partir de la existencia de A.  
  
 Cada regla está asociada a una probabilidad derivada de los datos de compatibilidad. Estas probabilidades resultan útiles al realizar recomendaciones. Por ejemplo, es posible que solo desee ver las reglas que tienen al menos un 50 por ciento de probabilidad de ser precisas, basándose en datos existentes.  
  
 El informe muestra los conjuntos de elementos encontrados ordenados por la mejora respecto al modelo predictivo. La mejora respecto al modelo predictivo es una puntuación que le indica la importancia del conjunto de elementos.  
  
|Columna del informe|¿Qué indica|  
|----------------------|-----------------------|  
|Existing Items|Muestra los elementos necesarios para realizar una recomendación.<br /><br /> En la minería de datos, estos elementos se dice que en el *lado izquierdo* de la regla de asociación.|  
|Predicted Item|Muestra el elemento que se va a recomendar.<br /><br /> En la minería de datos, estos elementos se dice que en el *derecha* de la regla de asociación.|  
|Probabilidad|Muestra la probabilidad de que esta regla sea correcta.|  
|Soporte técnico|Indica el número de casos en los datos existentes que constituyen una prueba para esta regla.|  
|Rule Value|Si proporciona un valor para los elementos de la cesta de compras, esta columna calcula el valor de la predicción basándose en el costo de los elementos.|  
|Mejora respecto al modelo predictivo|Indica la fuerza de la correlación entre los elementos de la primera columna y los elementos de la segunda columna. También se denomina *importancia*.<br /><br /> Una mejora respecto al modelo predictivo de 0 significa que no hay ninguna correlación. Un valor positivo significa que los elementos de la primera columna predicen el elemento de la segunda columna. Cuanto más alto sea el número, más fuerte será la correlación.|  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 El Cliente de minería de datos para Excel, que es un complemento independiente que proporciona funciones más avanzadas de minería de datos, también incluye un asistente que realiza análisis de asociación. Para obtener más información, consulte [Asistente asociar &#40;cliente de minería de datos para Excel&#41;](associate-wizard-data-mining-client-for-excel.md).  
  
 Para obtener más información sobre el algoritmo usado para realizar este análisis, vea el tema sobre el algoritmo de asociación de Microsoft en los Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tablas para Excel](table-analysis-tools-for-excel.md)  
  
  
