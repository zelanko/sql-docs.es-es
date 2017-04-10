---
title: "Sintaxis (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "expresiones [Integration Services], sintaxis"
  - "sintaxis [Integration Services]"
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 48
---
# Sintaxis (SSIS)
  La sintaxis de expresiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es similar a la sintaxis de los lenguajes C y C#. Las expresiones incluyen elementos como identificadores (columnas y variables), literales, operadores y funciones. En este tema se resumen los requisitos únicos de la sintaxis del evaluador de expresiones cuando se aplican a distintos elementos de una expresión.  
  
> [!NOTE]  
>  En las versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], había un límite de 4000 caracteres para el resultado de la evaluación de una expresión cuando el resultado tenía el tipo de datos DT_WSTR o DT_STR de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se ha quitado este límite.  
  
 Para conocer expresiones de ejemplo que usen funciones y operadores específicos, vea el tema sobre cada operador y función en los temas: [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
 Para ver expresiones de ejemplo que usen varios operadores y funciones, así como identificadores y literales, vea [Ejemplos de expresiones avanzadas de Integration Services](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md).  
  
 Para ver expresiones de ejemplo que se pueden usar en expresiones de propiedad, vea [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## Identificadores  
 Las expresiones pueden incluir identificadores de columnas y variables. Las columnas pueden originarse en el origen de datos o crearse mediante transformaciones del flujo de datos. Las expresiones pueden usar identificadores de linaje para hacer referencia a columnas. Los identificadores de linaje son números que identifican de forma única los elementos de un paquete. Para hacer referencia a estos indicadores en una expresión, debe incluirse el prefijo #. Por ejemplo, para hacer referencia al identificador de linaje 138, debe utilizarse #138.  
  
 Las expresiones pueden incluir las variables del sistema proporcionadas por [!INCLUDE[ssIS](../../includes/ssis-md.md)] y variables personalizadas. Para hacer referencia a estas variables en una expresión, debe incluirse el prefijo @. Por ejemplo, para hacer referencia a la variable `Counter` , debe utilizar @Counter. El carácter @ no forma parte del nombre de la variable; solamente indica al evaluador de expresiones que el identificador es una variable. Para obtener más información, vea [Identificadores &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
## Literales  
 Las expresiones pueden incluir literales numéricos, de cadena y booleanos. Los literales de cadena usados en expresiones deben escribirse entre comillas. Los literales numéricos y booleanos no utilizan comillas. El lenguaje de expresiones incluye secuencias de escape para los caracteres que se suelen marcar con caracteres de escape. Para obtener más información, vea [Literales &#40;SSIS&#41;](../../integration-services/expressions/literals-ssis.md).  
  
## Operadores  
 El evaluador de expresiones proporciona un conjunto de operadores que proporciona funcionalidad similar a la de los operadores de lenguajes como Transact-SQL, C++ y C#. Sin embargo, el lenguaje de expresiones incluye operadores adicionales y utiliza símbolos distintos a los usuales. Para obtener más información, vea [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md).  
  
### Operador de resolución de espacio de nombres  
 Las expresiones usan el operador de resolución de espacio de nombres (::) para eliminar la ambigüedad de las variables que tienen el mismo nombre. Con el operador de resolución de espacio de nombres puede calificar la variable con su espacio de nombres, lo que permite usar varias variables con el mismo nombre en un paquete.  
  
#### Operador de conversión  
 El operador de conversión convierte resultados de expresiones, valores de columna, valores de variable y constantes de un tipo de datos a otro. El operador de conversión proporcionado por el lenguaje de expresiones es similar al proporcionado por los lenguajes C y C#. En Transact-SQL, las funciones CAST y CONVERT proporcionan esta funcionalidad. La sintaxis del operador de conversión difiere de la utilizada en CAST y CONVERT en los siguientes aspectos:  
  
-   Puede utilizar una expresión como un argumento.  
  
-   Su sintaxis no incluye la palabra clave CAST.  
  
-   Su sintaxis no incluye la palabra clave AS.  
  
##### Operador condicional  
 El operador condicional devuelve una de dos expresiones, en función de la evaluación de una expresión booleana. El operador condicional proporcionado por el lenguaje de expresiones es similar al proporcionado por los lenguajes C y C#. En expresiones multidimensionales (MDX), la función IIF proporciona una funcionalidad similar.  
  
###### Operadores lógicos  
 El lenguaje de expresiones admite el carácter ! para el operador lógico NOT. En Transact-SQL, el operador ! está integrado en el conjunto de operadores relacionales. Por ejemplo, Transact-SQL proporciona los operadores > y !>. El lenguaje de expresiones [!INCLUDE[ssIS](../../includes/ssis-md.md)] no admite la combinación del operador ! y otros operadores. Por ejemplo, no se permite combinar ! y > en ! >. Sin embargo, el lenguaje de expresiones admite una combinación de caracteres != integrada para la comparación "distinto de".  
  
###### Operadores de igualdad  
 La gramática del evaluador de expresiones proporciona el operador de igualdad ==. Este operador es el equivalente del operador = de Transact-SQL y el operador == de C#.  
  
## Funciones  
 El lenguaje de expresiones incluye funciones de fecha y hora, funciones matemáticas y funciones de cadena similares a las funciones de Transact-SQL y los métodos de C#.  
  
 Unas cuantas funciones se llaman igual que las funciones de Transact-SQL, pero tienen una funcionalidad ligeramente distinta en el evaluador de expresiones.  
  
-   En Transact-SQL, la función ISNULL reemplaza valores NULL por un valor especificado, mientras que la función ISNULL del evaluador de expresiones devuelve un valor booleano en función de si una expresión es NULL.  
  
-   En Transact-SQL, la función ROUND incluye la opción de truncar el conjunto de resultados, mientras que la función ROUND del evaluador de expresiones no ofrece esta opción.  
  
 Para obtener más información, vea [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
## Tareas relacionadas  
 [utilizar una expresión en un componente de flujo de datos](../Topic/Use%20an%20Expression%20in%20a%20Data%20Flow%20Component.md)  
  
## Contenido relacionado  
  
-   Artículo técnico, sobre la [referencia rápida de expresiones de SSIS](http://go.microsoft.com/fwlink/?LinkId=746575), en pragmaticworks.com  
  
-   Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
  