---
title: "Literales (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "string literals"
  - "numéricos, literales [Integration Services]"
  - "booleanos, literales"
  - "expresiones [Integration Services], literales"
  - "literales [Integration Services]"
  - "asignar literales [Integration Services]"
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Literales (SSIS)
 Las expresiones pueden incluir literales numéricos, de cadena y booleanos. El evaluador de expresiones admite diversos literales numéricos tales como constantes enteras, decimales y de punto flotante. El evaluador de expresiones también admite sufijos que indican valor largo o de tipo flotante, con los que se especifica cómo controla el evaluador de expresiones los valores, y notación científica en literales numéricos.  
  
## <a name="numeric-literals"></a>Literales numéricos  
 El evaluador de expresiones admite tipos de datos numéricos enteros y no enteros. También admite los identificadores de linaje (los identificadores numéricos únicos de los elementos de un paquete). Los identificadores de linaje son números, pero no se pueden usar en operaciones matemáticas.  
  
 El evaluador de expresiones admite sufijos, que puede utilizar para especificar cómo debe tratar el evaluador de expresiones el literal numérico. Por ejemplo, puede indicar que el entero 37 se debe tratar como un tipo de datos de entero largo escribiendo 37L o 37l.  
  
 En la tabla siguiente se muestran los sufijos para literales numéricos.  
  
|Sufijo|Description|  
|------------|-----------------|  
|L o l|Literal numérico largo.|  
|U o u|Literal numérico sin signo.|  
|E o e|Exponente en notación científica|  
  
 En la tabla siguiente se muestran elementos de expresiones numéricas y sus expresiones regulares.  
  
|Elemento de expresión|Expresión regular|Description|  
|------------------------|------------------------|-----------------|  
|Dígitos expresados como D.|[0-9]|Cualquier dígito.|  
|Notación científica expresada como E.|[Ee][+-]?{D}+|Mayúsculas o minúsculas y, opcionalmente, + o -, y uno o más dígitos tal como se define en D.|  
|Sufijo de entero expresado como IS.|(([lL]?[uU]?)&#124;([uU]?[lL]?))|Opcionalmente, u y l o una combinación de u y l en mayúsculas o minúsculas. U o u indica un valor sin signo. L o l indica un valor largo.|  
|Sufijo de tipo flotante expresado como FS.|([f&#124;F]&#124;[l&#124;L])|f o l en mayúsculas o minúsculas. F o f indica un valor de punto flotante (tipo de datos DT_R4). L o l indica un valor largo (tipo de datos DT_R8).|  
|Dígito hexadecimal expresado como H.|[a-fA-F0-9]|Cualquier dígito hexadecimal.|  
  
 En la tabla siguiente se describen literales numéricos válidos mediante el lenguaje de expresiones regulares.  
  
|Expresión regular|Description|  
|------------------------|-----------------|  
|{D}+{IS}|Literal numérico entero con al menos un dígito (D) y, opcionalmente, el sufijo de valor largo o sin signo (IS).  Ejemplos: 457, 785u, 986L y 7945ul.|  
|{D}+{E}{FS}|Literal numérico no entero con al menos un dígito (D), notación científica y el sufijo de valor largo o de tipo flotante.  Ejemplos: 4E8l, 13e-2f y 5E+L.|  
|{D}*"."{D}+{E}?{FS}|Literal numérico no entero con una posición decimal, una fracción decimal con al menos un dígito (D), un exponente opcional (E) y un identificador de valor de punto flotante o largo (FS). Este literal numérico tiene el tipo de datos DT_R4 o DT_R8.  Ejemplos: 6,45E3f, 0,89E-2l y 1,05E+7F.|  
|{D}+"."{D}*{E}?{FS}|Literal numérico no entero con al menos un dígito significativo (D), una posición decimal, un exponente (E) y un identificador de valor largo o de punto flotante (FS). Este literal numérico tiene el tipo de datos DT_R4 o DT_R8.  Ejemplos: 1,E-4f, 4,6E6L y 8,365E+2f.|  
|{D}*.{D}+|Literal numérico no entero con precisión y escala. Tiene una posición decimal y una fracción decimal con al menos un dígito (D). Este literal numérico tiene el tipo de datos DT_NUMERIC.  Ejemplos: 0,9, 5,8 y 0,346.|  
|{D}+.{D}*|Literal numérico no entero con precisión y escala. Tiene al menos un dígito significativo (D) y una posición decimal. Este literal numérico tiene el tipo de datos DT_NUMERIC.  Ejemplos: 6,0, 0,2 y 8,0.|  
|#{D}+|Identificador de linaje. Consta del carácter de número (#) y al menos un dígito (D). Ejemplos: #123.|  
|0[xX]{H}+{uU}|Literal numérico en formato hexadecimal. Incluye un cero, una x en mayúsculas o minúsculas, al menos una H en mayúsculas y, opcionalmente, el sufijo de valor sin signo. Ejemplos: 0xFF0A y 0X000010000U.|  
  
 Para obtener más información sobre los tipos de datos usados por el evaluador de expresiones, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Las expresiones pueden incluir literales numéricos con distintos tipos de datos. Cuando el evaluador de expresiones evalúa estas expresiones, convierte los datos a tipos compatibles. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 Sin embargo, la conversión entre algunos tipos de datos requiere una conversión de tipos explícita. El evaluador de expresiones proporciona el operador de conversión para realizar la conversión explícita de tipos de datos. Para obtener más información, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>Asignar literales numéricos a tipos de datos de Integration Services  
 El evaluador de expresiones realiza las siguientes conversiones al evaluar literales numéricos:  
  
-   Un literal numérico entero se asigna a un tipo de datos entero de la manera siguiente.  
  
    |Sufijo|Tipo de resultado|  
    |------------|-----------------|  
    |None|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **IMPORTANTE** Si falta el sufijo de valor largo (L o l), el evaluador de expresiones asignará valores con signo al tipo de datos DT_I4 y valores sin signo al tipo de datos DT_UI4, aunque el valor desborde el tipo de datos.  
  
-   Un literal numérico que incluya un exponente se convertirá al tipo de datos DT_R4 o DT_R8. Si la expresión incluye el sufijo largo, se convierte a DT_R8; si incluye el sufijo de tipo flotante, se convierte al tipo de datos DT_R4.  
  
-   Si un literal numérico no entero incluye F o f, se asigna al tipo de datos DT_R4. Si incluye L o l y el número es un entero, se asigna al tipo de datos DT_I8. Si es un número real, se asigna al tipo de datos DT_R8. Si incluye el sufijo de valor largo, se convierte al tipo de datos DT_R8.  
  
-   Un literal numérico no entero con precisión y escala se asigna al tipo de datos DT_NUMERIC.  
  
## <a name="string-literals"></a>Literales de cadena  
 Los literales de cadena deben escribirse entre comillas. El lenguaje de expresiones proporciona un conjunto de secuencias de escape para caracteres, como los caracteres no imprimibles y las comillas, que se suelen marcar con caracteres de escape.  
  
 Un literal de cadena consta de cero o más caracteres entrecomillados. Si una cadena contiene comillas, deberá marcarlas con caracteres de escape para que se pueda analizar la expresión. En una cadena se admite cualquier carácter de dos bytes, con la excepción de \x0000, que es el terminador NULL de una cadena.  
  
 Las cadenas pueden incluir otros caracteres que requieran una secuencia de escape. En la tabla siguiente se muestran secuencias de escape para literales de cadena.  
  
|Secuencia de escape|Description|  
|---------------------|-----------------|  
|\a|Alerta|  
|\b|Retroceso|  
|\f|Avance de página|  
|\n|Nueva línea|  
|\r|Retorno de carro|  
|\t|Tabulación horizontal|  
|\v|Tabulación vertical|  
|\\"|Comillas|  
|\\\|Barra diagonal inversa|  
|\xhhhh|Carácter Unicode en notación hexadecimal|  
  
## <a name="boolean-literals"></a>Literales booleanos  
 El evaluador de expresiones admite los literales booleanos habituales: **True** y **False**. El evaluador de expresiones no distingue mayúsculas de minúsculas; cualquier combinación de mayúsculas y minúsculas es válida. Por ejemplo, TRUE es tan válido como True.  
  
> **NOTA:** en una expresión, un literal booleano debe estar delimitado por espacios.  
  
  