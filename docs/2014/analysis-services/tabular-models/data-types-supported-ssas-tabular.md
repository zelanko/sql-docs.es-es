---
title: Tipos de datos compatibles (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 083eff2195b0c8099ec4fdfb80e7224e1d42d135
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086905"
---
# <a name="data-types-supported-ssas-tabular"></a>Tipos de datos compatibles (SSAS tabular)
  En este artículo se describen los tipos de datos que se pueden usar en los modelos tabulares, así como la conversión implícita de los tipos de datos cuando los datos se calculan o se usan en una fórmula DAX (Expresiones de análisis de datos).  
  
 Este artículo contiene las secciones siguientes:  
  
-   [Tipos de datos usados en los modelos tabulares](#bkmk_data_types)  
  
-   [Conversiones implícitas y explícitas de tipos de datos en fórmulas de DAX](#bkmk_implicit)  
  
-   [Controlar valores en blanco, cadenas vacías y valores cero](#bkmk_hand_blanks)  
  
##  <a name="bkmk_data_types"></a> Tipos de datos usados en los modelos tabulares  
 Se admiten los tipos de datos siguientes. Cuando se importan datos o se usa un valor en una fórmula, incluso si el origen de datos contiene un tipo de datos distinto, los datos se convierten a uno de los siguientes tipos de datos. Los datos que se producen como resultado de las fórmulas también usan estos tipos de datos.  
  
 En general, estos tipos de datos se implementan para permitir cálculos precisos en columnas calculadas y, para mantener la coherencia, se aplican las mismas restricciones al resto de los datos de los modelos.  
  
 Los formatos usados para números, moneda, fechas y horas deben seguir el formato de la configuración regional especificada en el equipo cliente que se usa para trabajar con los datos del modelo. Se pueden usar las opciones de formato en el modelo para controlar la forma en que se muestra el valor.  
  
||||  
|-|-|-|  
|Tipo de datos en el modelo|Tipo de datos en DAX|Descripción|  
|Whole Number|Valor entero de 64 bits (ocho bytes) <sup>1, 2</sup>|Números que no tienen posiciones decimales. Los enteros pueden ser números positivos o negativos, pero deben ser números enteros comprendidos entre -9.223.372.036.854.775.808 (-2^63) y 9.223.372.036.854.775.807 (2^63-1).|  
|Decimal Number|Número real de 64 bits (ocho bytes) <sup>1, 2</sup>|Los números reales son aquellos que pueden tener posiciones decimales. Abarcan un amplio intervalo de valores:<br /><br /> Valores negativos de -1,79E +308 a -2,23E -308<br /><br /> Cero<br /><br /> Valores positivos desde 2,23E -308 hasta 1,79E + 308<br /><br /> Sin embargo, el número de dígitos significativos se limita a 17 dígitos decimales.|  
|Booleano|Boolean|Valor True o False.|  
|Texto|String|Cadena de datos de carácter Unicode. Pueden ser cadenas, números o fechas representados en un formato de texto.|  
|date|Fecha y hora|Fechas y horas en una representación de fecha y hora aceptada.<br /><br /> Las fechas válidas son todas las fechas posteriores al 1 de marzo de 1900.|  
|Moneda|Moneda|El tipo de datos de moneda permite los valores comprendidos entre -922.337.203.685.477,5808 y 922.337.203.685.477,5807 con cuatro dígitos decimales de precisión fija.|  
|N/D|En blanco|Un tipo en blanco es un tipo de datos de DAX que representa y reemplaza los valores NULL de SQL. Un valor en blanco se puede crear con la función BLANK y se puede comprobar si es tal con la función lógica ISBLANK.|  
  
 <sup>1</sup> las fórmulas DAX no admiten tipos de datos que son menores que los enumerados en la tabla.  
  
 <sup>2</sup> si intenta importar datos con valores numéricos muy elevados, puede producir un error de importación con el siguiente error:  
  
 Error de base de datos en memoria: el '\<nombre de columna >' columna de la '\<nombre de tabla >' tabla contiene un valor, ' 1.7976931348623157e + 308', que no se admite. La operación se ha cancelado.  
  
 Este error se produce porque el diseñador de modelos utiliza ese valor para representar los valores NULL. Los valores de la siguiente lista son sinónimos del valor NULL mencionado anteriormente:  
  
||  
|-|  
|Valor|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 Debería quitar de nuevo el valor de los datos e intentar volver a importarlo.  
  
> [!NOTE]  
>  No puede importar de una columna **varchar(max)** que contenga una longitud de cadena superior a 131 072 caracteres.  
  
### <a name="table-data-type"></a>Tipo de datos de tabla  
 Además, DAX usa un tipo de datos de *tabla* . DAX usa este tipo de datos en muchas funciones, como agregaciones y cálculos de inteligencia de tiempo. Algunas funciones requieren una referencia a una tabla y otras devuelven una tabla que se puede usar como entrada para otras funciones. En algunas funciones que requieren una tabla como entrada, puede especificar una expresión que se evalúa como una tabla; para otras funciones, se requiere una referencia a una tabla base. Para obtener información sobre los requisitos de funciones concretas, vea [Referencia de funciones DAX](https://msdn.microsoft.com/library/ee634396.aspx).  
  
##  <a name="bkmk_implicit"></a> Conversiones implícitas y explícitas de tipos de datos en fórmulas de DAX  
 Cada función DAX tiene requisitos concretos acerca de los tipos de datos que se usan como entradas y salidas. Por ejemplo, algunas funciones requieren enteros para algunos argumentos y fechas para otros; otras funciones requieren texto o tablas.  
  
 Si los datos de la columna que especifique como argumento son incompatibles con el tipo de datos requerido por la función, en muchos casos DAX devolverá un error. No obstante, siempre que sea posible DAX intentará convertir implícitamente los datos al tipo requerido. Por ejemplo:  
  
-   Puede escribir un número, por ejemplo, “123”, como una cadena. DAX analizará la cadena e intentará especificarla como tipo de datos numérico.  
  
-   Se pueden sumar TRUE + 1 y obtener el resultado 2, ya que TRUE se convierte implícitamente al número 1 y se realiza la operación 1+1.  
  
-   Si suma los valores de dos columnas y uno está representado como texto ("12") y el otro como número (12), DAX convierte implícitamente la cadena a un número y, a continuación, realiza la suma para obtener un resultado numérico. La expresión siguiente devuelve 44: = "22" + 22  
  
-   Si intenta concatenar dos números, el complemento de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] los presentará como cadenas y, después, los concatenará. La expresión siguiente devuelve  "1234": = 12 & 34  
  
 En la tabla siguiente se resumen las conversiones implícitas de tipo de datos que se realizan en las fórmulas. En general, el diseñador de modelos semánticos se comporta como Microsoft Excel y, siempre que sea posible, realiza conversiones implícitas cuando lo requiere la operación especificada.  
  
### <a name="table-of-implicit-data-conversions"></a>Tabla de conversiones de datos implícitas  
 El tipo de conversión que se realiza está determinada por el operador, que convierte los valores que requiere antes de realizar la operación solicitada. En estas tablas se enumeran los operadores y se indica la conversión que se lleva a cabo en cada tipo de datos de la columna cuando se empareja con el tipo de datos de la fila de intersección.  
  
> [!NOTE]  
>  Los tipos de datos de texto no se incluyen en estas tablas. Cuando un número se representa en formato de texto, en algunos casos, el diseñador de modelos intentará determinar el tipo de número y representarlo como un número.  
  
#### <a name="addition-"></a>Suma (+)  
  
||||||  
|-|-|-|-|-|  
|Operador (+)|INTEGER|Moneda|real|Fecha y hora|  
|INTEGER|INTEGER|Moneda|real|Fecha y hora|  
|Moneda|Moneda|Moneda|real|Fecha y hora|  
|real|real|real|real|Fecha y hora|  
|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|  
  
 Por ejemplo, si se usa un número real en una operación de suma en combinación con datos de moneda, ambos valores se convierten en REAL y el resultado se devuelve como REAL.  
  
#### <a name="subtraction--"></a>Resta (-)  
 En la siguiente tabla el encabezado de fila es el minuendo (el lado de la izquierda) y el encabezado de columna es el substraendo (el lado de la derecha).  
  
||||||  
|-|-|-|-|-|  
|Operador (-)|INTEGER|Moneda|real|Fecha y hora|  
|INTEGER|INTEGER|Moneda|real|real|  
|Moneda|Moneda|Moneda|real|real|  
|real|real|real|real|real|  
|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|Fecha y hora|  
  
 Por ejemplo, si se usa una fecha en una operación de resta con otro tipo de datos, ambos valores se convierten en fechas y el valor devuelto también es una fecha.  
  
> [!NOTE]  
>  Los modelos tabulares también admiten el operador unario - (negativo), pero este operador no cambia el tipo de datos del operando.  
  
#### <a name="multiplication-"></a>Multiplicación (*)  
  
||||||  
|-|-|-|-|-|  
|Operador (*)|INTEGER|Moneda|real|Fecha y hora|  
|INTEGER|INTEGER|Moneda|real|INTEGER|  
|Moneda|Moneda|real|Moneda|Moneda|  
|real|real|Moneda|real|real|  
  
 Por ejemplo, si un entero se combina con un número real en una operación de multiplicación, ambos números se convierten a números reales y el valor devuelto también es REAL.  
  
#### <a name="division-"></a>División (/)  
 En la siguiente tabla, el encabezado de fila es el numerador y el encabezado de columna es el denominador.  
  
||||||  
|-|-|-|-|-|  
|Operador (/)<br /><br /> (Fila/Columna)|INTEGER|Moneda|real|Fecha y hora|  
|INTEGER|real|Moneda|real|real|  
|Moneda|Moneda|real|Moneda|real|  
|real|real|real|real|real|  
|Fecha y hora|real|real|real|real|  
  
 Por ejemplo, si un entero se combina con un valor de moneda en una operación de división, ambos valores se convierten a números reales y el resultado también es un número real.  
  
#### <a name="comparison-operators"></a>Operadores de comparación  
 En las expresiones de comparación, los valores booleanos se consideran mayores que los valores de cadena y los valores de cadena se consideran mayores que los valores numéricos o de fecha u hora; se considera que los números y los valores de fecha u hora tienen el mismo rango. No se realiza ninguna conversión implícita para los valores booleanos o de cadena; BLANK o un valor en blanco se convierte en 0/""/false, según el tipo de datos del otro valor comparado.  
  
 Las siguientes expresiones de DAX muestran este comportamiento:  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")`, devuelve `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")`, devuelve `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")`, devuelve `"Expression is false"`  
  
 Las conversiones se realizan implícitamente para los tipos numéricos o de fecha y hora, tal y como se describe en la siguiente tabla:  
  
||||||  
|-|-|-|-|-|  
|Operador de comparación|INTEGER|Moneda|real|Fecha y hora|  
|INTEGER|INTEGER|Moneda|real|real|  
|Moneda|Moneda|Moneda|real|real|  
|real|real|real|real|real|  
|Fecha y hora|real|real|real|Fecha y hora|  
  
##  <a name="bkmk_hand_blanks"></a> Controlar valores en blanco, cadenas vacías y valores cero  
 La forma en que DAX trata los valores cero, los valores NULL y las cadenas vacías es distinta a como lo hacen Microsoft Excel y SQL Server. En esta sección se describen las diferencias y cómo se tratan estos tipos de datos.  
  
 Lo importante es recordar que, un valor en blanco, una celda vacía o la ausencia de un valor se representan por el nuevo tipo de valor: BLANK. Depende de cada función el modo en que se tratan en las operaciones, como suma o concatenación. También se pueden generar valores en blanco con la función BLANK o comprobar los valores en blanco con la función ISBLANK. Los valores NULL de base de datos no se admiten en un modelo semántico y se convierten implícitamente a valores en blanco si en una fórmula de DAX se hace referencia a una columna que contiene un valor NULL.  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>Definir valores en blanco, valores NULL y cadenas vacías  
 En la tabla siguiente se resumen las diferencias entre DAX y Microsoft Excel con respecto al modo en que se tratan los valores en blanco.  
  
||||  
|-|-|-|  
|Expresión|DAX|Excel|  
|BLANK + BLANK|En blanco|0 (cero)|  
|BLANK +5|5|5|  
|BLANK * 5|En blanco|0 (cero)|  
|5/BLANK|Infinito|Error|  
|0/BLANK|NaN|Error|  
|BLANK/BLANK|En blanco|Error|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|En blanco|Error|  
|BLANK AND BLANK|BLANK|Error|  
  
 Para obtener información detallada sobre cómo una determinada función u operador trata los valores en blanco, vea los temas de cada función DAX en la sección [Referencia de funciones DAX](https://msdn.microsoft.com/library/ee634396.aspx).  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos &#40;Tabular de SSAS&#41;](../data-sources-ssas-tabular.md)   
 [Importar datos &#40;Tabular de SSAS&#41;](../import-data-ssas-tabular.md)  
  
  
