---
title: Compatibilidad de las fórmulas DAX en el modo DirectQuery (SSAS 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2014
ms.assetid: de83cfa9-9ffe-4e24-9c74-96a3876cb4bd
caps.latest.revision: 3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68a73fd64b9bba02a917c8538f79062ff85afbdb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189482"
---
# <a name="dax-formula-compatibility-in-directquery-mode-ssas-2014"></a>Compatibilidad de las fórmulas DAX en el modo DirectQuery (SSAS 2014)
El lenguaje de expresiones de análisis de datos (DAX) puede usarse para crear medidas y otras fórmulas personalizadas para su uso en los modelos tabulares de Analysis Services, [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] modelos de datos en los libros de Excel y modelos de datos de Power BI Desktop. En todos los sentidos, los modelos crean en estos entornos son idénticos, y puede usar el mismo medidas, relaciones y los KPI, etcetera. Sin embargo, si se crea un modelo Tabular de Analysis Services e implementarlo en el modo DirectQuery, hay algunas restricciones en las fórmulas que puede usar. En este tema proporciona información general sobre estas diferencias, se enumera las funciones que no se admiten en el modelo de tabulars de SQL Server 2014 Analysis Services en el nivel de compatibilidad 1100 o 1103 y en el modo DirectQuery, y enumera las funciones que se admiten pero puede ser devolver resultados diferentes.  
  
En este tema, utilizaremos el término *modelo en memoria* para hacer referencia a los modelos tabulares, que son totalmente hospedadas en memoria los datos almacenados en caché en un servidor de Analysis Services que se ejecuta en modo Tabular. Usamos *los modelos DirectQuery* para hacer referencia a los modelos tabulares que se han creado y/o implementado en modo DirectQuery. Para obtener información sobre el modo DirectQuery, vea [el modo DirectQuery (SSAS Tabular)](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5).  
  
  
## <a name="bkmk_SemanticDifferences"></a>Diferencias entre en memoria y el modo DirectQuery  
Las consultas en un modelo implementado en el modo DirectQuery pueden devolver unos resultados distintos a los que devolvería el mismo modelo implementado en el modo en memoria. Esto es porque con DirectQuery, se consultan los datos directamente desde un almacén de datos relacionales y las agregaciones necesarias para las fórmulas se llevan a cabo mediante el motor relacional correspondiente, en lugar de utilizar el motor de análisis en memoria xVelocity (VertiPaq) para el almacenamiento y cálculo.  
  
Por ejemplo, existen diferencias en la manera en la que determinados almacenes de datos relacionales procesan los valores numéricos, las fechas, los valores NULL, etc.  
  
En cambio, el lenguaje DAX intenta emular con la mayor fidelidad posible el comportamiento de las funciones de Microsoft Excel. Por ejemplo, al procesar los valores NULL, las cadenas vacías y los valores cero, Excel intenta proporcionar la mejor respuesta independientemente del tipo de datos preciso y, por lo tanto, el motor xVelocity actúa de igual manera. Sin embargo, cuando se implementa un modelo tabular en el modo DirectQuery y dicho modelo pasa fórmulas a un origen de datos relacional para su evaluación, los datos se deben procesar de acuerdo con la semántica del origen de datos relacional, que normalmente requiere un tratamiento distinto de las cadenas vacías frente a nulas. Por este motivo, la misma fórmula puede devolver resultados diferentes cuando se evalúa con los datos en caché y con los datos obtenidos exclusivamente del almacén relacional.  
  
Además, algunas funciones no se pueden utilizar en absoluto en el modo DirectQuery porque el cálculo necesitaría que los datos en el contexto actual se envían al origen de datos relacional como parámetro. Por ejemplo, las medidas en un [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] libro suelen emplear funciones de inteligencia de tiempo que hacen referencia a intervalos de fechas disponibles dentro del libro. Normalmente, estas fórmulas no se pueden utilizar en el modo DirectQuery.  
  
## <a name="semantic-differences"></a>Diferencias semánticas  
En esta sección se enumeran los tipos de diferencias semánticas que puede encontrar, y se describen las limitaciones que se pueden aplicar al uso de las funciones o a los resultados de las consultas.  
  
### <a name="bkmk_Comparisons"></a>Comparaciones  
En los modelos en memoria, DAX admite comparaciones de dos expresiones que dan como resultado valores escalares de tipos de datos diferentes. Sin embargo, los modelos que se implementan en el modo DirectQuery utilizan los tipos de datos y los operadores de comparación del motor relacional y, por lo tanto, pueden devolver resultados diferentes.  
  
Las siguientes comparaciones siempre devolverán un error si se usan en cálculos en un origen de datos DirectQuery:  
  
-   Tipo de datos numérico comparado con cualquier tipo de datos de cadena  
  
-   Tipo de datos numérico comparado con un valor booleano  
  
-   Cualquier tipo de datos de cadena comparado con un valor booleano  
  
En general, DAX es más permisivo con los errores de tipo de datos en los modelos en memoria, e intentará realizar una conversión implícita de valores un máximo de dos veces, tal y como se describe en esta sección. Sin embargo, las fórmulas que se envían a un almacén de datos relacional en el modo DirectQuery se evalúan de forma más estricta, siguiendo las reglas del motor relacional, y es más probable que generen errores.  
  
**Comparaciones de cadenas y números**  
EJEMPLO: `“2” < 3`  
  
La fórmula compara una cadena de texto con un número. La expresión es **true** tanto en el modo DirectQuery como en los modelos en memoria.  
  
En un modelo en memoria, el resultado es **true** porque los números especificados como cadenas se convierten implícitamente en un tipo de datos numérico con el fin de realizar comparaciones con otros números. SQL también convierte implícitamente números de texto en números para realizar comparaciones con tipos de datos numéricos.  
  
Cabe decir que esto representa un cambio de comportamiento con respecto a la primera versión de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], que devolvería **false**, ya que el texto “2” se consideraría siempre mayor que cualquier número.  
  
**Comparación de cadenas de texto con valores booleanos**  
EJEMPLO: `“VERDADERO” = TRUE`  
  
Esta expresión compara una cadena de texto con un valor booleano. En general, en los modelos en memoria o DirectQuery, la comparación de un valor de cadena con un valor booleano genera un error. Las únicas excepciones a esta regla se producen cuando la cadena contiene las palabras **true** o **false**; si la cadena contiene un valor true o false, se realiza una conversión a un valor booleano y se lleva a cabo la comparación proporcionando el resultado lógico.  
  
**Comparación de valores NULL**  
EJEMPLO: `EVALUATE ROW("X", BLANK() = BLANK())`  
  
Esta fórmula compara el equivalente a un valor NULL en SQL con un valor NULL. Devuelve **true** en los modelos en memoria y DirectQuery; en el modelo DirectQuery, se realiza una previsión que garantiza un comportamiento similar al del modelo en memoria.  
  
Tenga en cuenta que en Transact-SQL, un valor NULL nunca es igual a otro valor NULL. Sin embargo, en DAX, un espacio en blanco es igual a otro espacio en blanco. Este comportamiento es el mismo para todos los modelos en memoria. Es importante destacar que el modo DirectQuery utiliza generalmente la semántica de SQL Server; pero en este caso no lo hace, proporcionando un nuevo comportamiento para las comparaciones de valores NULL.  
  
### <a name="bkmk_Casts"></a>Conversiones de tipos  
  
No hay ninguna función de conversión como tal en DAX, pero las conversiones implícitas se realizan en muchas operaciones aritméticas y de comparación. Es la operación aritmética o de comparación la que determina el tipo de datos del resultado. Por ejemplo,  
  
-   Los valores booleanos se tratan como numéricos en las operaciones aritméticas, como TRUE + 1, o la función MIN aplicada a una columna de valores booleanos. Una operación NOT también devuelve un valor numérico.  
  
-   Los valores booleanos siempre se tratan como valores lógicos en las comparaciones y cuando se usan con EXACT, AND, OR, &amp;&amp;o ||.  
  
**Conversión de valores de cadena en valores booleanos**  
En los modelos en memoria y DirectQuery, solo se permiten las conversiones de las cadenas siguientes en valores booleanos: **“”** (cadena vacía), **“true”**, **“false”**; donde una cadena vacía se convierte en un valor false.  
  
Las conversiones de cualquier otra cadena al tipo de datos booleano producirán un error.  
  
**Conversión de valores de cadena en valores de fecha y hora**  
En el modo DirectQuery, las conversiones de representaciones de cadena de fechas y horas en valores **datetime** reales se comportan de la misma manera que en SQL Server.  
  
Para obtener información acerca de las reglas que rigen las conversiones de cadena a **datetime** tipos de datos de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] modelos, vea el [sintaxis de DAX](https://msdn.microsoft.com/library/ee634217.aspx).  
  
Los modelos que utilizan el almacén de datos en memoria admiten una gama más limitada de formatos de texto para fechas que los formatos de cadena para fechas que admite SQL Server. Sin embargo, DAX admite formatos de fecha y hora personalizados.  
  
**Conversión de valores de cadena en otros valores no booleanos**  
Cuando se realiza la conversión de cadenas en valores no booleanos, el modo DirectQuery se comporta igual que SQL Server. Para más información, vea [CAST y CONVERT (Transact-SQL)](http://msdn.microsoft.com/en-us/a87d0850-c670-4720-9ad5-6f5a22343ea8).  
  
**No se permite la conversión de números en cadenas**  
EJEMPLO: `CONCATENATE(102,”,345”)`  
  
La conversión de números en cadenas no se admite en SQL Server.  
  
Esta fórmula devuelve un error en los modelos tabulares y en el modo DirectQuery, pero genera un resultado en [!INCLUDE[ssGemini](../includes/ssgemini-md.md)].  
  
**No se admiten las conversiones de dos intentos en DirectQuery**  
A menudo, los modelos en memoria intentan una segunda conversión si se produce un error en la primera. Esto nunca sucede en el modo DirectQuery.  
  
EJEMPLO: `TODAY() + “13:14:15”`  
  
En esta expresión, el primer parámetro tiene el tipo **datetime** y el segundo parámetro, el tipo **string**. Sin embargo, las conversiones se tratan de forma diferente al combinar los operandos. DAX realizará una conversión implícita de **string** a **double**. En los modelos en memoria, el motor de las fórmulas intenta realizar la conversión directamente en **double**y, si esto no es posible, intentará convertir la cadena en **datetime**.  
  
En el modo DirectQuery, solo se aplicará la conversión directa de **string** en **double** . Si no es posible realizar esta conversión, la fórmula devolverá un error.  
  
### <a name="bkmk_Math"></a>Funciones matemáticas y operaciones aritméticas  
Algunas funciones matemáticas devolverán resultados diferentes en el modo DirectQuery debido a diferencias en el tipo de datos subyacente o en la conversión que se puede aplicar en las operaciones. Asimismo, las restricciones descritas anteriormente en el intervalo de valores permitidos pueden afectar al resultado de las operaciones aritméticas.  
  
**Orden de adición**  
Al crear una fórmula que agrega una serie de números, un modelo en memoria podría procesar los números en un orden distinto al de un modelo DirectQuery.  Por lo tanto, si dispone de muchos números positivos y negativos muy grandes, es posible que obtenga un error en una operación y resultados correctos en otra.  
  
**Uso de la función POWER**  
EJEMPLO: `POWER(-64, 1/3)`  
  
En el modo DirectQuery, la función POWER no puede utilizar valores negativos como base cuando se eleva a un exponente fraccionario. Este es el comportamiento previsto de SQL Server.  
  
En un modelo en memoria, la fórmula devuelve -4.  
  
**Operaciones de desbordamiento numérico**  
En Transact-SQL, las operaciones que dan como resultado un desbordamiento numérico devuelven un error de desbordamiento; por lo tanto, las fórmulas que producen un desbordamiento también generan un error en el modo DirectQuery.  
  
Sin embargo, si se utiliza la misma fórmula en un modelo en memoria, esta devuelve un entero de ocho bytes. Esto se debe a que el motor de fórmulas no realiza comprobaciones de desbordamientos numéricos.  
  
**Las funciones LOG con valores en blanco devuelven resultados diferentes**  
SQL Server procesa los valores NULL y los valores en blanco de forma diferente a como lo hace el motor xVelocity. En consecuencia, la siguiente fórmula devuelve un error en el modo DirectQuery, pero devuelve infinito (–inf) en el modo en memoria.  
  
`EXAMPLE: LOG(blank())`  
  
Las mismas limitaciones se aplican al resto de funciones logarítmicas: LOG10 y LN.  
  
Para más información sobre el tipo de datos **blank** de DAX, vea see [Especificación de sintaxis de DAX](https://msdn.microsoft.com/library/ee634217.aspx).  
  
**División por 0 y división por un valor en blanco**  
En el modo DirectQuery, la división por cero (0) o la división por un valor en blanco siempre producirá un error. SQL Server no admite la noción de infinito y, dado que el resultado natural de una división por 0 es infinito, el resultado es un error. Sin embargo, SQL Server admite la división por valores NULL, y el resultado siempre deberá ser un valor NULL.  
  
En lugar de devolver resultados diferentes para estas operaciones, en el modo DirectQuery, ambos tipos de operaciones (la división por cero y la división por valores NULL) devuelven un error.  
  
Tenga en cuenta que, tanto en Excel como en los modelos de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , la división entre cero también devuelve un error. La división por un valor en blanco devuelve un valor en blanco.  
  
Las expresiones siguientes son todas válidas en los modelos en memoria, pero producirán un error en el modo DirectQuery:  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
La expresión `BLANK/BLANK` es un caso especial que devuelve `BLANK` tanto en los modelos en memoria como en el modo DirectQuery.  
  
### <a name="bkmk_Ranges"></a>Intervalos numéricos y de fecha y hora admitidos  
Las fórmulas de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] y los modelos tabulares en memoria están sujetos a las mismas limitaciones que Excel con respecto al máximo los valores permitidos para números reales y las fechas. Sin embargo, pueden surgir diferencias cuando se devuelve el valor máximo de un cálculo o de una consulta, o cuando se convierten, redondean o truncan los valores.  
  
-   En el modo DirectQuery, si se multiplican valores de los tipos **Currency** y **Real** y el resultado es mayor que el valor máximo posible, no se genera ningún error y se devuelve un valor NULL.  
  
-   En los modelos en memoria, no se genera ningún error, pero se devuelve el valor máximo.  
  
En general, dado que los intervalos de fechas aceptados son diferentes para Excel y para SQL Server, los resultados solo coincidirán si las fechas se encuentran dentro del intervalo de fechas común, que incluye las fechas siguientes:  
  
-   Fecha más antigua: 1 de marzo de 1990  
  
-   Fecha más reciente: 31 diciembre de 9999  
  
Si cualquiera de las fechas utilizadas en las fórmulas queda fuera de este intervalo, la fórmula generará un error o los resultados no coincidirán.  
  
**Valores de coma flotante admitidos por CEILING**  
EJEMPLO: `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
El equivalente en Transact-SQL de la función DAX CEILING solo admite valores con magnitudes de 10^19 o inferiores. Una regla general es que los valores de coma flotante tienen que caber en **bigint**.  
  
**Funciones Datepart con fechas que están fuera del intervalo**  
Los resultados en el modo DirectQuery solo coincidirán con los resultados de los modelos en memoria cuando la fecha utilizada como argumento se encuentre en el intervalo de fechas válido. Si no se cumplen estas condiciones, pueden suceder dos cosas: que se genere un error o que los resultados devueltos por la fórmula en DirectQuery sean diferentes de los obtenidos en el modo en memoria.  
  
EJEMPLO: `MONTH(0)` o `YEAR(0)`  
  
En el modo DirectQuery, las expresiones devuelven 12 y 1899, respectivamente.  
  
En los modelos en memoria, las expresiones devuelven 1 y 1900, respectivamente.  
  
EJEMPLO:  `EOMONTH(0.0001, 1)`  
  
Los resultados de esta expresión solo coincidirán cuando los datos proporcionados como parámetro se encuentren dentro del intervalo de fechas válido.  
  
EJEMPLO: `EOMONTH(blank(), blank())` o `EDATE(blank(), blank())`  
  
Los resultados de esta expresión deben coincidir en el modo DirectQuery y en el modo en memoria.  
  
**Truncamiento de los valores de hora**  
EJEMPLO: `SECOND(1231.04097222222)`  
  
En el modo DirectQuery, el resultado se trunca, de acuerdo con las reglas de SQL Server, y la expresión se evalúa como 59.  
  
En los modelos en memoria, los resultados de cada operación provisional se redondean; por lo tanto, la expresión se evalúa como 0.  
  
A continuación se explica cómo se calcula este valor:  
  
1.  La fracción de la entrada (0,04097222222) se multiplica por 24.  
  
2.  El valor de hora resultante (0,98333333328) se multiplica por 60.  
  
3.  El valor de minuto resultante es 58,9999999968.  
  
4.  La fracción del valor de minuto (0,9999999968) se multiplica por 60.  
  
5.  El valor de segundo resultante (59.999999808) se redondea a 60.  
  
6.  60 equivale a 0.  
  
**El tipo de datos Time de SQL no se admite**  
En los modelos en memoria no se puede usar el nuevo tipo de datos **Time** de SQL. En el modo DirectQuery, las fórmulas que hagan referencia a columnas con este tipo de datos devolverán un error. Las columnas de con datos Time no se pueden importar en un modelo en memoria.  
  
Sin embargo, en [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] en algunos casos en los modelos almacenados en caché, el motor convierte el valor de tiempo para un tipo de datos aceptable y la fórmula devuelve un resultado.  
  
Este comportamiento afecta a todas las funciones que utilizan una columna de fecha como parámetro.  
  
### <a name="bkmk_Currency"></a>Currency  
En el modo DirectQuery, si el resultado de una operación aritmética tiene el tipo **Currency**, el valor ha de estar dentro del siguiente rango:  
  
-   Mínimo: -922337203685477.5808  
  
-   Máximo: 922337203685477.5807  
  
**Combinar tipos de datos de moneda y REAL**  
EJEMPLO: `Currency sample 1`  
  
Si los tipos **Currency** y **Real** se multiplican y el resultado es mayor que 9223372036854774784 (0x7ffffffffffffc00), el modo DirectQuery no generará un error.  
  
En un modelo en memoria, se generará un error si el valor absoluto del resultado es mayor que 922337203685477.4784.  
  
**Operaciones cuyo resultado es un valor que está fuera del intervalo**  
EJEMPLO: `Currency sample 2`  
  
Si las operaciones realizadas con dos valores de moneda cualesquiera dan como resultado un valor que está fuera del intervalo especificado, se generará un error en los modelos en memoria, pero no en los modelos DirectQuery.  
  
**Combinar datos de moneda con otros tipos de datos**  
La división de valores de moneda por valores de otros tipos numéricos puede dar lugar a resultados diferentes.  
  
### <a name="bkmk_Aggregations"></a>Funciones de agregación  
Las funciones estadísticas en una tabla con una fila devuelven resultados diferentes. Las funciones de agregación realizadas en tablas vacías también se comportan de forma diferente en los modelos en memoria de como lo hacen en el modo DirectQuery.  
  
**Funciones estadísticas en una tabla con una sola fila**  
Si la tabla que se utiliza como argumento contiene una sola fila, en el modo DirectQuery, las funciones estadísticas como STDEV y VAR devolverán un valor NULL.  
  
En un modelo en memoria, una fórmula que utilice STDEV o VAR en una tabla con una sola fila devuelve un error de división por cero.  
  
### <a name="bkmk_Text"></a>Funciones de texto  
Puesto que los almacenes de datos relacionales proporcionan tipos de datos de texto diferentes de los de Excel, es posible que se muestren resultados distintos al buscar cadenas o trabajar con subcadenas. Asimismo, la longitud de las cadenas puede ser diferente.  
  
En general, las funciones de manipulación de cadenas que utilicen columnas de tamaño fijo como argumentos pueden tener resultados diferentes.  
  
Además, en SQL Server, algunas funciones de texto admiten argumentos adicionales que no se proporcionan en Excel. Si la fórmula requiere el argumento que falta, es posible que se obtengan resultados diferentes o errores en el modelo en memoria.  
  
**Las operaciones que devuelven un carácter mediante las funciones LEFT, RIGHT, etc. pueden devolver el carácter correcto pero en minúsculas o mayúsculas, o no devolver ningún resultado**  
EJEMPLO: `LEFT([“text”], 2)`  
  
En el modo DirectQuery, el formato de mayúsculas o minúsculas que se devuelve es siempre exactamente el mismo que el de la letra almacenada en la base de datos. Sin embargo, el motor xVelocity utiliza un algoritmo diferente para la compresión y la indización de valores con objeto de mejorar el rendimiento.  
  
De forma predeterminada, se utiliza la intercalación Latin1_General, que no distingue entre mayúsculas y minúsculas pero que sí distingue los acentos. Por lo tanto, si hay varias instancias de una cadena de texto en minúsculas, mayúsculas o en ambas, todas las instancias se consideran la misma cadena, y solo la primera de ellas se almacena en el índice. Todas las funciones de texto que actúan sobre cadenas almacenadas recuperarán la porción especificada de la forma indizada. Por lo tanto, la fórmula del ejemplo devolverá el mismo valor para toda la columna, utilizando la primera instancia como entrada.  
  
[Almacenamiento e intercalación de cadenas en modelos tabulares](http://msdn.microsoft.com/en-us/8516f0ad-32ee-4688-a304-e705143642ca)  
  
Este comportamiento también se aplica a otras funciones de texto, incluyendo RIGHT, MID, etc.  
  
**La longitud de la cadena influye en los resultados**  
EJEMPLO: `SEARCH(“within string”, “sample target  text”, 1, 1)`  
  
Si busca una cadena mediante la función SEARCH, y la cadena de destino es más larga que la cadena original, el modo DirectQuery genera un error.  
  
En un modelo en memoria, se devuelve la cadena buscada, pero con su longitud truncada a la longitud del &lt;texto original&gt;.  
  
EJEMPLO: `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
En el modo DirectQuery, si la longitud de la cadena de reemplazo es mayor que la longitud de la cadena original, la fórmula devuelve un valor NULL.  
  
En los modelos en memoria, la fórmula sigue el comportamiento de Excel, que concatena la cadena de origen y la de reemplazo, lo que devuelve CACalifornia.  
  
**TRIM implícito en el centro de las cadenas**  
EJEMPLO: `TRIM(“ A sample sentence with leading white space”)`  
  
El modo DirectQuery traduce la función DAX TRIM a la instrucción `LTRIM(RTRIM(<column>))`de SQL. Como resultado, solo se quitan los caracteres de espacio en blanco iniciales y finales.  
  
En cambio, la misma fórmula en un modelo en memoria quita los espacios situados dentro de la cadena, siguiendo el comportamiento de Excel.  
  
**RTRIM implícito con uso de la función LEN**  
EJEMPLO: `LEN(‘string_column’)`  
  
Al igual que SQL Server, el modo DirectQuery quita automáticamente el espacio en blanco del final de las columnas de cadena: es decir, realiza un RTRIM implícito. Por lo tanto, las fórmulas que utilizan la función LEN pueden devolver valores diferentes si la cadena tiene espacios finales.  
  
**In-memory admite parámetros adicionales para SUBSTITUTE**  
EJEMPLO: `SUBSTITUTE([Title],”Doctor”,”Dr.”)`  
  
EJEMPLO: `SUBSTITUTE([Title],”Doctor”,”Dr.”, 2)`  
  
En el modo DirectQuery, solo se puede puede utilizar la versión de esta función que tiene tres (3) parámetros: una referencia a una columna, el texto antiguo y el texto nuevo. Si se utiliza la segunda fórmula, se genera un error.  
  
En los modelos en memoria, puede utilizar un cuarto parámetro opcional para especificar el número de repetición de la cadena que desea reemplazar. Por ejemplo, puede reemplazar solo la segunda repetición, etc.  
  
**Restricciones en las longitudes de cadena para las operaciones REPT**  
En los modelos en memoria, la longitud de una cadena que resulta de una operación REPT debe ser inferior a 32.767 caracteres.  
  
Esta limitación no se aplica en el modo DirectQuery.  
  
**Las operaciones de subcadena devuelven resultados diferentes en función del tipo de carácter**  
EJEMPLO: `MID([col], 2, 5)`  
  
Si el texto de entrada es **varchar** o **nvarchar**, el resultado de la fórmula es siempre el mismo.  
  
Pero, en el modo DirectQuery, si el texto es un carácter de longitud fija y el valor para *&lt;num_chars&gt;* es mayor que la longitud de la cadena de destino, se anexará un espacio en blanco al final de la cadena resultante.  
  
En un modelo en memoria, el resultado termina en el último carácter de la cadena, sin relleno.  
  
## <a name="bkmk_SupportedFunc"></a>Funciones admitidas en el modo DirectQuery  
Se pueden utilizar las funciones DAX siguientes en el modo DirectQuery, pero con las restricciones descritas en la sección anterior.  
  
**Funciones de texto**  
  
CONCATENATE  
  
FIND  
  
LEFT  
  
LEN  
  
MID  
  
REPLACE  
  
REPT  
  
RIGHT  
  
SUBSTITUTE  
  
TRIM  
  
**Funciones estadísticas**  
  
COUNT  
  
STDEV.P  
  
STDEV.S  
  
STDEVX.P  
  
STDEVX.S  
  
VAR.P  
  
VAR.S  
  
VARX.P  
  
VARX.S  
  
**Funciones de fecha y hora**  
  
DATE  
  
EDATE  
  
EOMONTH  
  
DATE  
  
TIME  
  
SECOND  
  
**Funciones matemáticas y número**  
  
CEILING  
  
LN  
  
LOG  
  
LOG10  
  
POWER  
  
**Consultas de tablas de DAX**  
  
Existen algunas limitaciones al evaluar fórmulas en un modelo DirectQuery mediante consultas de tablas de DAX. DirectQuery no admite que se haga referencia dos veces a la misma columna en una cláusula ORDER BY. La instrucción equivalente en Transact-SQL no se puede crear y la consulta produce un error.  
  
En un modelo en memoria, la repetición de la cláusula ORDER no influye en los resultados.  
  
## <a name="bkmk_NotSupportedFunc"></a>Funciones no admitidas en el modo DirectQuery  
Algunas funciones DAX no se admiten en los modelos implementados en el modo DirectQuery. Los motivos por los que una determinada función no se admite pueden ser uno o varios de los siguientes:  
  
-   El motor relacional subyacente no puede realizar cálculos equivalentes a los realizados por el motor xVelocity.  
  
-   La fórmula no se puede convertir en una expresión SQL equivalente.  
  
-   El rendimiento de la expresión convertida y de los cálculos resultantes sería inaceptable.  
  
Las funciones DAX siguientes no se pueden utilizar en los modelos DirectQuery.  
  
**Funciones de ruta de acceso**  
  
PATH  
  
PATHCONTAINS  
  
PATHITEM  
  
PATHITEMREVERSE  
  
PATHLENGTH  
  
**Funciones adicionales**  
  
COUNTBLANK  
  
FIXED  
  
FORMAT  
  
RAND  
  
RANDBETWEEN  
  
**Funciones de inteligencia de tiempo: fechas de inicio y finalización**  
  
DATESQTD  
  
DATESYTD  
  
DATESMTD  
  
DATESQTD  
  
DATESINPERIOD  
  
TOTALMTD  
  
TOTALQTD  
  
TOTALYTD  
  
DATESINPERIOD  
  
SAMEPERIODLASTYEAR  
  
PARALLELPERIOD  
  
**Las funciones de inteligencia de tiempo: saldos**  
  
OPENINGBALANCEMONTH  
  
OPENINGBALANCEQUARTER  
  
OPENINGBALANCEYEAR  
  
CLOSINGBALANCEMONTH  
  
CLOSINGBALANCEQUARTER  
  
CLOSINGBALANCEYEAR  
  
**Funciones de inteligencia de tiempo: períodos anteriores y siguientes**  
  
PREVIOUSDAY  
  
PREVIOUSMONTH  
  
PREVIOUSQUARTER  
  
PREVIOUSYEAR  
  
NEXTDAY  
  
NEXTMONTH  
  
NEXTQUARTER  
  
NEXTYEAR  
  
**Funciones de inteligencia de tiempo: períodos y cálculos durante períodos**  
  
STARTOFMONTH  
  
STARTOFQUARTER  
  
STARTOFYEAR  
  
ENDOFMONTH  
  
ENDOFQUARTER  
  
ENDOFYEAR  
  
FIRSTDATE  
  
LASTDATE  
  
DATEADD  
  
## <a name="see-also"></a>Vea también  
[Modo DirectQuery (SSAS tabular)](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  

