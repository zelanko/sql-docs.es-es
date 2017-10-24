---
title: "La sintaxis de filtros y ejemplos de modelos (Analysis Services: minería de datos) | Documentos de Microsoft"
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
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c24c6ad5bbfba2f93039bd53609ddd86010e10ee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>Sintaxis y ejemplos del filtro de modelos (Analysis Services: Minería de datos)
  En esta sección se proporciona información detallada sobre la sintaxis para los filtros de modelo, junto con expresiones de ejemplo.  
  
 [Sintaxis de filtro](#bkmk_Syntax)  
  
 [Filtros en atributos de casos](#bkmk_Ex1)  
  
 [Filtros en atributos de tabla anidada](#bkmk_Ex2)  
  
 [Filtros en varios atributos de tabla anidada](#bkmk_Ex3)  
  
 [Faltan atributos de filtros en una tabla anidada](#bkmk_Ex4)  
  
 [Filtros en varios valores de tabla anidada](#bkmk_Ex5)  
  
 [Filtros en los atributos de tabla anidada y EXISTS](#bkmk_Ex6)  
  
 [Combinaciones de filtro](#bkmk_Ex7)  
  
 [Filtros en fechas](#bkmk_Ex8)  
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 Las expresiones de filtro generalmente equivalen al contenido de una cláusula WHERE. Puede conectar varias condiciones usando los operadores lógicos **AND**, **OR**y **NOT**.  
  
 En tablas anidadas, también puede usar los operadores **EXISTS** y **NOT EXISTS** . Una condición **EXISTS** se evalúa como **true** si la subconsulta devuelve al menos una fila. Esto es útil en casos en los que desea restringir el modelo a los casos que contienen un valor determinado en la tabla anidada: por ejemplo, los clientes que han comprado un artículo al menos una vez.  
  
 Una condición **NOT EXISTS** se evalúa como **true** si la condición especificada en la subconsulta no existe. Un ejemplo es cuando se desea restringir el modelo a los clientes que nunca han comprado un artículo determinado.  
  
 La sintaxis general es la siguiente:  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 Contiene uno o más predicados, conectados por operadores lógicos.  
  
 *lista de predicados*  
 Una o más expresiones de filtro válidas, separadas por operadores lógicos.  
  
 *columnName*  
 El nombre de una columna de estructura de minería de datos.  
  
 operador lógico  
 **AND**, **OR**, **NOT**  
  
 *avPredicate*  
 Expresión de filtro que solamente se puede aplicar a una columna de estructura de minería de datos escalar. Una expresión *avPredicate* se puede usar en ambos filtros de modelos o filtros de tablas anidadas.  
  
 Una expresión que usa cualquiera de los operadores siguientes solo se puede aplicar a una columna continua. :  
  
-   **\<** (menor que)  
  
-   **>** (mayor que)  
  
-   **>=** (mayor o igual que)  
  
-   **\<=** (menor o igual que)  
  
> [!NOTE]  
>  Independientemente del tipo de datos, estos operadores no se pueden aplicar a una columna que tenga el tipo **Discrete**, **Discretized**o **Key**.  
  
 Una expresión que usa cualquiera de los operadores siguientes se puede aplicar a una columna de clave continua, discreta o de datos discretos:  
  
-   **=** (es igual a)  
  
-   **!=** (no es igual a)  
  
-   **IS NULL**  
  
 Si el argumento *avPredicate*se aplica a una columna de datos discretos, el valor usado en el filtro puede ser cualquier valor de un depósito concreto.  
  
 Es decir, no define la condición como `AgeDisc = ’25-35’`, pero en su lugar calcula y, a continuación, usa un valor de ese intervalo.  
  
 Ejemplo:  `AgeDisc = 27`  indica cualquier valor del mismo intervalo que 27, que en este caso es 25-35.  
  
 *nestedTablePredicate*  
 Expresión de filtro que se aplica a una tabla anidada. Solo se puede usar en filtros de modelos.  
  
 El argumento de subconsulta de *nestedTablePredicate*solamente se puede aplicar a una columna de estructura de minería de datos de tabla.  
  
 subconsulta  
 Instrucción SELECT seguida de un predicado válido o una lista de predicados.  
  
 Todos los predicados deben ser del tipo que se describe en *avPredicates*. Además, los predicados solo pueden hacer referencia a las columnas incluidas en la tabla anidada actual, identificadas por el argumento *columnName*.  
  
### <a name="limitations-on-filter-syntax"></a>Limitaciones en la sintaxis de filtro  
 A los filtros se les aplican las restricciones siguientes:  
  
-   Un filtro solamente puede contener predicados simples. Entre estos se incluyen operadores matemáticos, escalares y nombres de columna.  
  
-   No se admiten las funciones definidas por el usuario en la sintaxis del filtro.  
  
-   No se admiten los operadores no booleanos, como los signos más o menos, en la sintaxis del filtro.  
  
## <a name="examples-of-filters"></a>Ejemplos de filtros  
 Los ejemplos siguientes muestran el uso de filtros aplicados a un modelo de minería de datos. Si crea la expresión de filtro usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la ventana **Propiedad** y el panel **Expresión** del cuadro de diálogo de filtros, vería solamente la cadena que aparece después de las palabras clave WITH FILTER. Aquí, la definición de la estructura de minería de datos está incluida para facilitar la comprensión del uso y del tipo de columna.  
  
###  <a name="bkmk_Ex1"></a> Ejemplo 1: Filtrado de nivel de caso típico  
 Este ejemplo muestra un filtro simple que restringe los casos usados en el modelo a los clientes cuya profesión sea arquitecto y sean mayores de 30 años.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation=’Architect’)  
```  
  
  
###  <a name="bkmk_Ex2"></a> Ejemplo 2: filtrado de nivel de caso usando atributos de tabla anidada  
 Si su estructura de minería de datos contiene tablas anidadas, puede filtrar por la existencia de un valor en una tabla anidada o filtrar en filas de tabla anidada que contienen un valor concreto. Este ejemplo restringe los casos usados para el modelo a los clientes mayores de 30 años que realizaron al menos una compra que incluía la leche.  
  
 Como se muestra en este ejemplo, no es necesario que el filtro use solamente las columnas incluidas en el modelo. La tabla anidada **Products** forma parte de la estructura de minería de datos pero no está incluida en el modelo de minería de datos. Sin embargo, todavía puede filtrar por los valores y atributos de la tabla anidada. Para ver los detalles de estos casos, la obtención de detalles debe estar habilitada.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’)  
)  
```  
  
  
###  <a name="bkmk_Ex3"></a> Ejemplo 3: filtrado del nivel de caso en varios atributos de tabla anidada  
 En este ejemplo se muestra un filtro de tres partes: se aplica una condición a la tabla de casos, otra condición a un atributo de la tabla anidada y otra, en un valor concreto de una de las columnas de tabla anidada.  
  
 La primera condición del filtro, `Age > 30`, se aplica a una columna de la tabla de casos. Las condiciones restantes se aplican a la tabla anidada.  
  
 La segunda condición, `EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’`, comprueba la presencia de al menos una compra en la tabla anidada que incluía la leche. La tercera condición, `Quantity>=2`, significa que el cliente debe haber comprado al menos dos unidades de leche en una transacción única.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity >= 2)   
)  
```  
  
  
###  <a name="bkmk_Ex4"></a> Ejemplo 4: filtrado del nivel de caso en ausencia de atributos de tabla anidada  
 En este ejemplo se muestra cómo limitar los casos al cliente que no compró un artículo específico, filtrando por la ausencia de un atributo en la tabla anidada. En este ejemplo, el modelo se entrena usando clientes mayores de 30 años que nunca han comprado leche.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’) )  
```  
  
  
###  <a name="bkmk_Ex5"></a> Ejemplo 5: filtrado por varios valores de tabla anidada  
 El propósito del ejemplo es mostrar el filtrado de tabla anidada. El filtro de tabla anidada se aplica después del filtro de casos y solamente restringe las filas de tabla anidada.  
  
 Este modelo podría contener varios casos con tablas anidadas vacías porque no se especifica EXISTS.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
WITH DRILLTHROUGH  
```  
  
  
###  <a name="bkmk_Ex6"></a> Ejemplo 6: filtrar por los atributos de tabla anidada y EXISTS  
 En este ejemplo, el filtro en la tabla anidada restringe las filas a aquéllas que contienen leche o agua embotellada. A continuación, los casos del modelo se restringen usando una instrucción **EXISTS** . Esto asegura que la tabla anidada no está vacía.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
FILTER (EXISTS (Products))  
```  
  
  
###  <a name="bkmk_Ex7"></a> Ejemplo 7: combinaciones de filtros complejas  
 El escenario para este modelo se parece al del ejemplo 4 pero es mucho más complejo. La tabla anidada, **ProductsOnSale**, tiene la condición de filtro `(OnSale)` que significa que el valor de **OnSale** debe ser **true** para el producto enumerado en **ProductName**. Aquí, **OnSale** es una columna de estructura.  
  
 La segunda parte del filtro, para **ProductsNotOnSale**, repite esta sintaxis pero filtra por los productos para los que el valor de **OnSale** es **not true**`(!OnSale)`.  
  
 Finalmente, se combinan las condiciones y se agrega una restricción adicional a la tabla de casos. El resultado es predecir compras de productos en la lista **ProductsNotOnSale** , basándose en los casos incluidos en la lista **ProductsOnSale** , para todos los clientes mayores de 25.  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
###  <a name="bkmk_Ex8"></a> Ejemplo 8: filtrar según las fechas  
 Puede filtrar las columnas de entrada según fechas, como con cualquier otro dato. Las fechas contenidas en una columna del tipo de fecha y hora son valores continuos; por consiguiente, puede especificar un intervalo de fechas utilizando a operadores como mayor que (>) o menor que (<). Si el origen de datos no representa las fechas por un tipo de datos continuo, sino como valores discretos o de texto, no puede filtrar en un intervalo de fechas, sino que debe especificar valores discretos e individuales.  
  
 Sin embargo, no puede crear un filtro en la columna de fecha en un modelo del serie temporal si la columna de fecha utilizada para el filtro también es la columna de clave para el modelo. Eso se debe a que, en los modelos de series temporales y de agrupación en clústeres de secuencia, la columna de fecha podría tratarse como de tipo **KeyTime** o **KeySequence**.  
  
 Si necesita filtrar en fechas continuas en un modelo de serie temporal, puede crear una copia de la columna en la estructura de minería de datos y filtrar el modelo en la nueva columna.  
  
 Por ejemplo, la siguiente expresión representa un filtro en una columna de fecha de tipo **Continuous** que se ha agregado al modelo de previsión.  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  Observe que cualquier columna adicional que agregue al modelo podría afectar a los resultados. Por consiguiente, si no desea utilizar la columna en el cálculo de la serie, solo debería agregar la columna a la estructura de minería de datos y no al modelo. También puede establecer la marca de modelo de la columna en **PredictOnly** o en **Ignore**. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
 En el caso de otros tipos de modelo, puede utilizar fechas como criterios de entrada o como criterios de filtro igual que con cualquier otra columna. Sin embargo, si tiene que utilizar un nivel concreto de granularidad que un tipo de datos **Continuous** no admita, puede crear un valor derivado en el origen de datos utilizando expresiones para extraer la unidad que se usará en el filtro y el análisis.  
  
> [!WARNING]  
>  Cuando especifique fechas como criterios de filtro, debe usar el siguiente formato, independientemente del formato de fecha del sistema operativo actual: `mm/dd/yyyy`. Cualquier otro formato produce un error.  
  
 Por ejemplo, si desea filtrar los resultados del centro de llamada para mostrar solo los fines de semana, puede crear una expresión en la vista del origen de datos que extraiga el nombre del día de la semana para cada fecha y, a continuación, utilizar ese el valor de nombre de día de la semana para la entrada o como un valor discreto en el filtro. Recuerde solo que los valores repetidos pueden afectar al modelo, de modo que debiera utilizar únicamente una de las columnas y no la columna de fecha más el valor derivado.  
  
  
## <a name="see-also"></a>Vea también  
 [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

