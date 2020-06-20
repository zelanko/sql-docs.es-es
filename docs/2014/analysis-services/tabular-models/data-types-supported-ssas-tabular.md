---
title: Tipos de datos admitidos (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2502b65b1b13f8ed819c138fdfe429390a905a56
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939763"
---
# <a name="data-types-supported-ssas-tabular"></a>Tipos de datos compatibles (SSAS tabular)
  En este artículo se describen los tipos de datos que se pueden usar en los modelos tabulares, así como la conversión implícita de los tipos de datos cuando los datos se calculan o se usan en una fórmula DAX (Expresiones de análisis de datos).  
  
 Este artículo contiene las siguientes secciones:  
  
-   [Tipos de datos usados en los modelos tabulares](#bkmk_data_types)  
  
-   [Conversión implícita y explícita de tipos de datos en fórmulas DAX](#bkmk_implicit)  
  
-   [Controlar valores en blanco, cadenas vacías y valores cero](#bkmk_hand_blanks)  
  
##  <a name="data-types-used-in-tabular-models"></a><a name="bkmk_data_types"></a>Tipos de datos usados en los modelos tabulares  
 Se admiten los tipos de datos siguientes. Cuando se importan datos o se usa un valor en una fórmula, incluso si el origen de datos contiene un tipo de datos distinto, los datos se convierten a uno de los siguientes tipos de datos. Los datos que se producen como resultado de las fórmulas también usan estos tipos de datos.  
  
 En general, estos tipos de datos se implementan para permitir cálculos precisos en columnas calculadas y, para mantener la coherencia, se aplican las mismas restricciones al resto de los datos de los modelos.  
  
 Los formatos usados para números, moneda, fechas y horas deben seguir el formato de la configuración regional especificada en el equipo cliente que se usa para trabajar con los datos del modelo. Se pueden usar las opciones de formato en el modelo para controlar la forma en que se muestra el valor.  
  
||||  
|-|-|-|  
|Tipo de datos en el modelo|Tipo de datos en DAX|Descripción|  
|Whole Number|Valor entero de 64 bits (ocho bytes) <sup>1, 2</sup>|Números que no tienen posiciones decimales. Los enteros pueden ser números positivos o negativos, pero deben ser números enteros comprendidos entre -9.223.372.036.854.775.808 (-2^63) y 9.223.372.036.854.775.807 (2^63-1).|  
|Decimal Number|Número real de 64 bits (ocho bytes) <sup>1, 2</sup>|Los números reales son aquellos que pueden tener posiciones decimales. Abarcan un amplio intervalo de valores:<br /><br /> Valores negativos de -1,79E +308 a -2,23E -308<br /><br /> Cero<br /><br /> Valores positivos desde 2,23E -308 hasta 1,79E + 308<br /><br /> Sin embargo, el número de dígitos significativos se limita a 17 dígitos decimales.|  
|Boolean|Boolean|Valor True o False.|  
|Texto|String|Cadena de datos de carácter Unicode. Pueden ser cadenas, números o fechas representados en un formato de texto.|  
|Date|Fecha y hora|Fechas y horas en una representación de fecha y hora aceptada.<br /><br /> Las fechas válidas son todas las fechas posteriores al 1 de marzo de 1900.|  
|Moneda|Moneda|El tipo de datos de moneda permite los valores comprendidos entre -922.337.203.685.477,5808 y 922.337.203.685.477,5807 con cuatro dígitos decimales de precisión fija.|  
|N/D|En blanco|Un tipo en blanco es un tipo de datos de DAX que representa y reemplaza los valores NULL de SQL. Un valor en blanco se puede crear con la función BLANK y se puede comprobar si es tal con la función lógica ISBLANK.|  
  
 <sup>1</sup> las fórmulas Dax no admiten tipos de datos que son menores que los enumerados en la tabla.  
  
 <sup>2</sup> si intenta importar datos con valores numéricos muy grandes, es posible que se produzca el siguiente error en la importación:  
  
 Error de base de datos en memoria: la \<column name> columna ' ' de la \<table name> tabla ' ' contiene un valor, ' 1.7976931348623157 e + 308 ', que no se admite. La operación se ha cancelado.  
  
 Este error se produce porque el diseñador de modelos utiliza ese valor para representar los valores NULL. Los valores de la siguiente lista son sinónimos del valor NULL mencionado anteriormente:  
  
||  
|-|  
|Value|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 Debería quitar de nuevo el valor de los datos e intentar volver a importarlo.  
  
> [!NOTE]  
>  No puede importar de una columna **varchar(max)** que contenga una longitud de cadena superior a 131 072 caracteres.  
  
### <a name="table-data-type"></a>Tipo de datos de tabla  
 Además, DAX usa un tipo de datos de *tabla* . DAX usa este tipo de datos en muchas funciones, como agregaciones y cálculos de inteligencia de tiempo. Algunas funciones requieren una referencia a una tabla; otras funciones devuelven una tabla que puede usarse como entrada para otras funciones. En algunas funciones que requieren una tabla como entrada, puede especificar una expresión que se evalúa en una tabla; para algunas funciones, se requiere una referencia a una tabla base. Para información acerca de los requisitos de funciones específicas, consulte [Referencia de funciones DAX](/dax/dax-function-reference).  
  
##  <a name="implicit-and-explicit-data-type-conversion-in-dax-formulas"></a><a name="bkmk_implicit"></a>Conversión implícita y explícita de tipos de datos en fórmulas DAX  
 Cada función DAX tiene requisitos concretos según los tipos de datos que se usan como entradas y salidas. Por ejemplo, algunas funciones requieren enteros para algunos argumentos y fechas para otros; otras funciones requieren texto o tablas.  
  
 Si los datos de la columna que especifique como argumento son incompatibles con el tipo de datos requerido por la función, en muchos casos DAX devolverá un error. Sin embargo, siempre que sea posible, DAX intentará convertir implícitamente los datos en el tipo de datos necesario. Por ejemplo:  
  
-   Puede escribir un número, por ejemplo "123", como una cadena. DAX analizará la cadena e intentará especificarla como tipo de datos numérico.  
  
-   Puede sumar TRUE + 1 y obtener el resultado 2, ya que TRUE se convierte implícitamente al número 1 y se realiza la operación 1 + 1.  
  
-   Si agrega valores en dos columnas, y un valor se representa como texto ("12") y el otro como un número (12), DAX convierte implícitamente la cadena en un número y, a continuación, realiza la suma para obtener un resultado numérico. La expresión siguiente devuelve 44: = "22" + 22  
  
-   Si intenta concatenar dos números, el complemento de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] los presentará como cadenas y, después, los concatenará. La expresión siguiente devuelve  "1234": = 12 & 34  
  
 En la tabla siguiente se resumen las conversiones implícitas de tipo de datos que se realizan en las fórmulas. En general, el diseñador de modelos semánticos se comporta como Microsoft Excel y, siempre que sea posible, realiza conversiones implícitas cuando lo requiere la operación especificada.  
  
### <a name="table-of-implicit-data-conversions"></a>Tabla de conversiones de datos implícitas  
 El tipo de conversión que se realiza está determinado por el operador, que convierte los valores que necesita antes de realizar la operación solicitada. Estas tablas enumeran los operadores e indican la conversión que se ha realizado en cada tipo de datos en la columna cuando se vincula con el tipo de datos en la fila de intersección.  
  
> [!NOTE]  
>  Los tipos de datos de texto no se incluyen en estas tablas. Cuando un número se representa en formato de texto, en algunos casos, el diseñador de modelos intentará determinar el tipo de número y representarlo como un número.  
  
#### <a name="addition-"></a>Suma (+)  
  
||||||  
|-|-|-|-|-|  
|Operador (+)|INTEGER|MONEDA|REAL|Fecha y hora|  
|ENTERO|ENTERO|MONEDA|REAL|Fecha y hora|  
|CURRENCY|CURRENCY|MONEDA|real|Fecha y hora|  
|real|real|real|real|Fecha y hora|  
|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|  
  
 Por ejemplo, si se usa un número real en una operación de suma en combinación con los datos de moneda, ambos valores se convierten en REAL y el resultado se devuelve como REAL.  
  
#### <a name="subtraction--"></a>Resta (-)  
 En la siguiente tabla el encabezado de fila es el minuendo (el lado de la izquierda) y el encabezado de columna es el substraendo (el lado de la derecha).  
  
||||||  
|-|-|-|-|-|  
|Operador (-)|INTEGER|MONEDA|real|Fecha y hora|  
|INTEGER|INTEGER|MONEDA|real|real|  
|CURRENCY|MONEDA|MONEDA|real|real|  
|real|real|real|real|real|  
|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|  
  
 Por ejemplo, si se usa una fecha en una operación de resta con cualquier otro tipo de datos, ambos valores se convierten en fechas y el valor devuelto también es una fecha.  
  
> [!NOTE]  
>  Los modelos tabulares también admiten el operador unario - (negativo), pero este operador no cambia el tipo de datos del operando.  
  
#### <a name="multiplication-"></a>Multiplicación (*)  
  
||||||  
|-|-|-|-|-|  
|Operador (*)|INTEGER|MONEDA|real|Fecha y hora|  
|INTEGER|INTEGER|MONEDA|real|ENTERO|  
|CURRENCY|MONEDA|real|CURRENCY|MONEDA|  
|real|real|MONEDA|real|real|  
  
 Por ejemplo, si un entero se combina con un número real en una operación de multiplicación, ambos números se convierten a números reales y el valor devuelto también es REAL.  
  
#### <a name="division-"></a>División (/)  
 En la siguiente tabla, el encabezado de fila es el numerador y el encabezado de columna es el denominador.  
  
||||||  
|-|-|-|-|-|  
|Operador (/)<br /><br /> (Fila/Columna)|INTEGER|MONEDA|real|Fecha y hora|  
|ENTERO|REAL|MONEDA|real|real|  
|CURRENCY|MONEDA|real|MONEDA|real|  
|real|real|real|real|real|  
|Fecha y hora|real|real|real|REAL|  
  
 Por ejemplo, si un entero se combina con un valor de moneda en una operación de división, ambos números se convierten a números reales y el resultado es también un número real.  
  
#### <a name="comparison-operators"></a>Operadores de comparación  
 En las expresiones de comparación, los valores booleanos se consideran mayores que los valores de cadena y los valores de cadena se consideran mayores que los valores numéricos o de fecha u hora; se considera que los números y los valores de fecha u hora tienen el mismo rango. No se realizan conversiones implícitas para valores booleanos o de cadena; Un valor en blanco o EN BLANCO se convierte en 0 / "" / falso según el tipo de datos del otro valor comparado.  
  
 Las siguientes expresiones DAX muestran este comportamiento:  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")`, devuelve `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")`, devuelve `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")`, devuelve `"Expression is false"`  
  
 Las conversiones se realizan implícitamente para tipos de fecha y hora, o numéricos, como se describe en la tabla siguiente:  
  
||||||  
|-|-|-|-|-|  
|Operadores de comparación|ENTERO|MONEDA|real|Fecha y hora|  
|ENTERO|INTEGER|MONEDA|real|REAL|  
|CURRENCY|CURRENCY|MONEDA|real|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Fecha y hora|real|REAL|REAL|Fecha y hora|  
  
##  <a name="handling-of-blanks-empty-strings-and-zero-values"></a><a name="bkmk_hand_blanks"></a>Control de espacios en blanco, cadenas vacías y valores cero  
 La forma en que DAX trata los valores cero, los valores NULL y las cadenas vacías es distinta a como lo hacen Microsoft Excel y SQL Server. En esta sección se describen las diferencias y cómo se tratan estos tipos de datos.  
  
 Lo importante es recordar que, un valor en blanco, una celda vacía o la ausencia de un valor se representan por el nuevo tipo de valor: BLANK. Depende de cada función el modo en que se tratan en las operaciones, como suma o concatenación. También puede generar espacios en blanco con la función BLANK o probarlos con la función ISBLANK. Los valores NULL de base de datos no se admiten en un modelo semántico y se convierten implícitamente a valores en blanco si en una fórmula de DAX se hace referencia a una columna que contiene un valor NULL.  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>Definir valores en blanco, valores NULL y cadenas vacías  
 En la tabla siguiente se resumen las diferencias entre DAX y Microsoft Excel con respecto al modo en que se tratan los valores en blanco.  
  
||||  
|-|-|-|  
|Expresión|DAX|Excel|  
|EN BLANCO + EN BLANCO|BLANK|0 (cero)|  
|BLANK +5|5|5|  
|EN BLANCO * 5|BLANK|0 (cero)|  
|5/EN BLANCO|Infinito|Error|  
|0/EN BLANCO|NaN|Error|  
|EN BLANCO/EN BLANCO|BLANK|Error|  
|FALSO O EN BLANCO|FALSE|FALSE|  
|FALSO Y EN BLANCO|FALSE|FALSE|  
|VERDADERO O EN BLANCO|TRUE|TRUE|  
|VERDADERO Y EN BLANCO|FALSO|VERDADERO|  
|EN BLANCO O EN BLANCO|EN BLANCO|Error|  
|EN BLANCO Y EN BLANCO|BLANK|Error|  
  
 Para obtener información detallada sobre cómo una determinada función u operador trata los valores en blanco, vea los temas de cada función DAX en la sección [Referencia de funciones DAX](/dax/dax-function-reference).  
  
## <a name="see-also"></a>Consulte también  
 [Orígenes de datos &#40;SSAS tabular&#41;](../data-sources-ssas-tabular.md)   
 [Importar datos &#40;SSAS tabular&#41;](../import-data-ssas-tabular.md)  
  
  
