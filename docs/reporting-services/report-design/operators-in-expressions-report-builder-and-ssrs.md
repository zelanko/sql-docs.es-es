---
title: Usar operadores en expresiones (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4499e62cf8564705b96ec74d2598c311e0097709
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817103"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>Usar operadores en expresiones (Generador de informes y SSRS)
  Un operador es un símbolo que representa las acciones que se aplican a uno o a varios términos de una expresión. En una expresión, se pueden usar las categorías de operadores siguientes: aritméticos, de comparación, de concatenación, lógicos o bit a bit, y de desplazamiento de bits.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>Aritméticos  
 Los operadores aritméticos realizan operaciones matemáticas entre dos términos numéricos de una expresión.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|^|Eleva un número a la potencia de otro número.|  
|*|Multiplica dos números.|  
|/|Divide dos números y devuelve un resultado de coma flotante.|  
|\|Divide dos números y devuelve un resultado de número entero.|  
|Mod|Devuelve el resto entero de una división. Por ejemplo, 7 Mod 5 = 2 porque el resto de 7 dividido entre 5 es 2.|  
|+|Suma dos números.|  
|-|Devuelve la diferencia entre dos números o indica el valor negativo de un término numérico.|  
  
### <a name="comparison"></a>Comparación  
 Los operadores de comparación comprueban si dos expresiones son iguales.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|<|Menor que.|  
|\<=|Menor o igual que.|  
|>|Mayor que.|  
|>=|Mayor o igual que.|  
|=|Igual que.|  
|<>|No es igual a.|  
|Like|Determina si una cadena de caracteres específica coincide con un patrón especificado. Un patrón puede contener caracteres normales y caracteres comodín. Durante la operación de búsqueda de coincidencias de patrón, los caracteres normales deben coincidir exactamente con los caracteres especificados en la cadena de caracteres. Sin embargo, los caracteres comodín pueden coincidir con fragmentos arbitrarios de la cadena. El uso de caracteres comodín hace que el operador LIKE sea más flexible que los operadores de comparación de cadenas = y !=.<br /><br /> La tabla siguiente contiene una lista de los caracteres que se pueden usar como caracteres comodín:<br /><br /> %: cualquier cadena de cero o más caracteres.<br /><br /> _: cualquier carácter individual.<br /><br /> [ ]: cualquier carácter individual que se encuentre en el intervalo (por ejemplo, [a-f]) o en el conjunto (por ejemplo, [aeiou]) especificado.<br /><br /> [^]: cualquier carácter individual que no se encuentre en el intervalo (por ejemplo, [^a-f]) o en el conjunto (por ejemplo, [^aeiou]) especificado.|  
|Is|Compara dos referencias a objeto.|  
  
### <a name="string-concatenation"></a>Concatenación de cadenas  
 Los operadores de concatenación de cadenas anexan la segunda cadena a la primera en una expresión. Para las demás operaciones de cadena, use las funciones integradas.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|&|Concatena dos cadenas|  
|+|Concatena dos cadenas|  
  
### <a name="logical-and-bitwise"></a>Lógicos y bit a bit  
 Los operadores lógicos y bit a bit realizan manipulaciones lógicas entre dos términos enteros de una expresión.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|And|Realiza una conjunción lógica entre dos expresiones booleanas o una conjunción bit a bit entre dos expresiones numéricas.|  
|Not|Realiza una negación lógica de una expresión booleana o una negación bit a bit de una expresión numérica.|  
|o bien|Realiza una disyunción lógica entre dos expresiones booleanas o una disyunción bit a bit entre dos valores numéricos.|  
|Xor|Realiza una operación de exclusión lógica entre dos expresiones booleanas o una exclusión bit a bit entre dos expresiones numéricas.|  
|AndAlso|Realiza una conjunción lógica entre dos expresiones.|  
|OrElse|Realiza una disyunción lógica entre dos expresiones.|  
  
### <a name="bit-shift"></a>Desplazamiento de bits  
 Los operadores de desplazamiento de bits realizan manipulaciones de bits entre dos términos enteros de una expresión.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|<\<|Realiza un desplazamiento aritmético a la izquierda en un patrón de bits.|  
|>>|Realiza un desplazamiento aritmético a la derecha en un patrón de bits.|  
  
## <a name="see-also"></a>Ver también  
 [Expresión (cuadro de diálogo)](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Expresión &#40;cuadro de diálogo del Generador de informes&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
