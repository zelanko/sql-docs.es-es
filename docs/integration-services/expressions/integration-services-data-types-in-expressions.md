---
title: Tipos de datos de Integration Services en las expresiones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 29d8806e055088bbf659ecf52fcc7f1c12fdf846
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725318"
---
# <a name="integration-services-data-types-in-expressions"></a>Tipos de datos de Integration Services en las expresiones

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El evaluador de expresiones utiliza tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cuando los datos entran por primera vez en un flujo de datos de un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , el motor de flujo de datos convierte todos los datos de columna a un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los datos de columna ya utilizados por una expresión a un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Las expresiones usadas en las transformaciones División condicional y Columna derivada pueden hacer referencia a columnas, ya que forman parte de un flujo de datos que incluye datos de columna.  
  
## <a name="variables"></a>Variables  
 Las expresiones también pueden usar variables. Las variables tienen un tipo de datos Variant. El evaluador de expresiones convierte el tipo de datos de una variable de un subtipo Variant a un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] antes de evaluar la expresión. Las variables solo pueden usar un subconjunto de los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por ejemplo, una variable no puede usar un tipo de datos de Bloque de objetos binarios grandes (BLOB).  
  
 Para más información sobre tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y sobre la asignación de tipos de datos Variant a tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="literals"></a>Literales  
 Además, las expresiones pueden incluir literales de cadena, booleanos y numéricos. Para más información sobre cómo convertir literales numéricos en tipos de datos numéricos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Literales &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md).  
  
## <a name="strings"></a>Cadenas  
 Puede utilizar DT_STR o DT_WSTR como el tipo de valor devuelto de una expresión. Sin embargo, dentro de una expresión, solo se admite DT_WSTR, y los valores DT_STR se convierten en valores DT_WSTR. Este comportamiento tiene varias implicaciones al escribir una expresión.  
  
-   Dentro de una expresión, use NULL(DT_WSTR,...) en lugar de NULL(DT_STR,...). Para más información sobre esta función, vea [NULL &#40;expresión de SSIS&#41;](../../integration-services/expressions/null-ssis-expression.md).  
  
-   Dentro de una expresión, solo puede utilizar la función CAST para convertir un valor en el tipo DT_STR en la raíz de la expresión, es decir, cuando se devuelve el resultado final de la expresión. De lo contrario, utilice el tipo DT_WSTR dentro de la expresión.  
  
 Tenga en cuenta las expresiones en la siguiente captura de pantalla.  
  
 ![Tipos de datos String en expresiones de SSIS](../../integration-services/expressions/media/stringsinssisexpressions.png "String data types in SSIS expressions")  
  
1.  La primera expresión se ejecuta sin error porque la función NULL(DT_STR,...) es en el nivel raíz de la expresión.  
  
2.  La segunda expresión se ejecuta sin error porque usa NULL(DT_WSTR,...).  
  
3.  La tercera expresión genera un error porque utiliza NULL(DT_STR,...) dentro de la expresión.  
  
4.  La cuarta expresión se ejecuta sin error porque convierte el resultado de NULL(DT_STR,...) dentro de la expresión.  
  
     El evaluador de expresiones controla esta conversión de forma inteligente y convierte en DT_WSTR, no en DT_STR, porque reconoce que la operación no es en el nivel raíz de la expresión.  
  
 Los ejemplos siguientes muestran los efectos de la conversión.  
  
 ![Convertir cadenas en expresiones de SSIS](../../integration-services/expressions/media/stringsinssisexpressions2.png "Casting strings in SSIS expressions")  
  
1.  En la primera expresión, la conversión no es en el nivel raíz de la expresión. El evaluador de expresiones controla esta conversión de forma inteligente y convierte en DT_WSTR, no en DT_STR. La expresión devuelve DT_WSTR.  
  
2.  En la segunda expresión, la conversión es en el nivel raíz de la expresión. La expresión devuelve DT_STR.  
  
## <a name="implicit-data-conversion"></a>Conversión implícita de datos  
 Una conversión implícita de un tipo de datos tiene lugar cuando el evaluador de expresiones convierte automáticamente los datos de un tipo a otro. Por ejemplo, si se comparan datos de tipo **smallint** con datos de tipo **int**, antes de realizar la comparación, los datos de tipo **smallint** se convierten implícitamente al tipo **int** .  
  
 El evaluador de expresiones no puede realizar una conversión de datos implícita cuando los argumentos y operandos tienen tipos de datos incompatibles. Además, el evaluador de expresiones no puede convertir implícitamente cualquier valor a un valor booleano. En lugar de ello, los argumentos y operandos se deben convertir explícitamente utilizando el operador de conversión. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 En el siguiente diagrama se muestra el tipo de resultado de las conversiones implícitas de las operaciones binarias. La intersección de la columna y la fila en esta tabla es el tipo de resultado de una operación binaria con operandos de los tipos izquierdo (From) y derecho (To).  
  
 ![Conversión de tipos de datos implícitos entre tipos de datos](../../integration-services/expressions/media/mw-dts-impl-conver-02.gif "Implicit data type conversion between data types")  
  
 La intersección de un entero con signo y un entero sin signo es un entero con signo posiblemente más grande que cualquiera de los argumentos.  
  
 Los operadores comparan cadenas, fechas, booleanos y otros tipos de datos. Antes de que un operador compare dos valores, el evaluador de expresiones realizará determinadas conversiones implícitas. El evaluador de expresiones siempre convierte los literales de cadena al tipo de datos DT_WSTR y los literales booleanos al tipo de datos DT_BOOL. Interpreta todos los valores entrecomillados como cadenas. Los literales numéricos se convierten a uno de los tipos de datos numéricos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!NOTE]  
>  Los valores booleanos son valores lógicos, no son números. Aunque los valores booleanos pueden mostrarse como números en algunos entornos, no se almacenan como números, y varios lenguajes de programación representan los valores booleanos como valores numéricos de maneras diferentes, como sucede con los métodos de .NET Framework.  
>   
>  Por ejemplo, las funciones de conversión disponibles en Visual Basic convierten **True** en -1, pero el método **System.Convert.ToInt32** de .NET Framework convierte **True** en +1. El lenguaje de expresiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] convierte **True** en -1.  
>   
>  Para evitar errores o resultados inesperados, no debe escribirse código que se base en valores numéricos específicos para **True** y **False**. Siempre que sea posible, se debe restringir el uso de las variables booleanas a los valores lógicos para los que están diseñadas.  
  
 Para obtener más información, consulte los temas siguientes:  
  
-   [== &#40;Igual&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/equal-ssis-expression.md)  
  
-   [\!= &#40;Diferente&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/unequal-ssis-expression.md)  
  
-   [&#62; &#40;Mayor que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)  
  
-   [&#60; &#40;Menor que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/less-than-ssis-expression.md)  
  
-   [&#62;= &#40;Mayor o igual que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)  
  
-   [&#60;= &#40;Menor o igual que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)  
  
 Una función de un solo argumento devuelve un resultado con el mismo tipo de datos del argumento, con las siguientes excepciones:  
  
-   DAY, MONTH y YEAR aceptan una fecha y devuelven un resultado entero (DT_I4).  
  
-   ISNULL acepta una expresión con cualquier tipo de datos de [!INCLUDE[ssIS](../../includes/ssis-md.md)] y devuelve un resultado booleano (DT_BOOL).  
  
-   SQUARE y SQRT aceptan una expresión numérica y devuelven un resultado numérico no integral (DT_R8).  
  
 Si los argumentos tienen el mismo tipo de datos, el resultado es de ese tipo. La única excepción es el resultado de una operación binaria aplicada a dos valores con el tipo de datos DT_DECIMAL, que devuelve un resultado con el tipo de datos DT_NUMERIC.  
  
## <a name="requirements-for-data-used-in-expressions"></a>Requisitos de los datos que se utilizan en expresiones  
 El evaluador de expresiones admite todos los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sin embargo, en función de la operación o la función, los operandos y los argumentos requieren determinados tipos de datos. El evaluador de expresiones impone los siguientes requisitos de tipo de datos a los datos usados en expresiones:  
  
-   Los operandos usados en operaciones **lógicas** deben contener un valor booleano. Por ejemplo, ColumnaA > 1&&ColumnaB < 2.  
  
-   Los operandos usados en operaciones **matemáticas** deben contener un valor numérico. Por ejemplo, 23,75 * 4.  
  
-   Los operandos utilizados en operaciones de comparación, como operaciones lógicas y de igualdad, deben devolver tipos de datos compatibles.  
  
     Por ejemplo, una de las expresiones del ejemplo siguiente usa el tipo de datos DT_DBTIMESTAMPOFFSET:  
  
     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`  
  
     El sistema convierte la expresión, `(DT_DBDATE)"1999-10-12"`, en DT_DBTIMESTAMPOFFSET. El ejemplo devuelve TRUE porque la expresión convertida pasa a ser "1999-10-12 00:00:00.000 +00: 00", que no es igual que el valor de la otra expresión, `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`.  
  
-   Los argumentos pasados a funciones matemáticas deben devolver un tipo de datos numérico. Dependiendo de la función o la operación, puede ser necesario usar un tipo de datos numérico específico. Por ejemplo, la función HEX requiere un entero con o sin signo.  
  
-   Los argumentos pasados a funciones de cadena se deben evaluar con un tipo de datos de carácter: DT_STR o DT_WSTR. Por ejemplo, UPPER("flor"). Algunas funciones de cadena, como SUBSTRING, requieren argumentos enteros adicionales para la posición inicial y la longitud de la cadena.  
  
-   Los argumentos pasados a funciones de fecha y hora deben contener una fecha válida. Por ejemplo, DAY(GETDATE()). Algunas funciones, como DATEADD, requieren un argumento entero adicional para el número de días que la función agrega a una fecha.  
  
 Las operaciones que combinan un entero de ocho bytes sin signo y un entero con signo requieren una conversión explícita para definir el formato del resultado. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Los resultados de muchas operaciones y funciones tienen tipos de datos predeterminados. Pueden ser el tipo de datos del argumento o el tipo de datos al que el evaluador de expresiones convierte el resultado. Por ejemplo, el resultado de un operador lógico OR (||) es siempre un valor booleano, el resultado de la función ABS es el tipo de datos numérico del argumento y el resultado de la multiplicación es el tipo de datos numérico más pequeño que puede contener el resultado sin perder información. Para más información sobre los tipos de datos de los resultados, vea [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [utilizar una expresión en un componente de flujo de datos](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico, sobre la [referencia rápida de expresiones de SSIS](https://go.microsoft.com/fwlink/?LinkId=746575), en pragmaticworks.com  
  
-   Artículo técnico, sobre [ejemplos de expresiones SSIS](https://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
  
