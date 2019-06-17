---
title: Objeto las reglas de nomenclatura (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 64e04754fd4bc4a404854eb5260daddf543e3c2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65979960"
---
# <a name="object-naming-rules-analysis-services"></a>Normas de nomenclatura de objetos (Analysis Services)
  En este tema se describen las convenciones de nomenclatura de los objetos, así como las palabras y los caracteres reservados que no se pueden usar en ningún nombre de objeto, código o script en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a> Convenciones de nomenclatura  
 Cada objeto tiene una propiedad `Name` y `ID` que debe ser única dentro del ámbito de la colección primaria. Por ejemplo, dos dimensiones pueden tener el mismo nombre siempre y cuando cada una resida en una base de datos diferente.  
  
 Aunque puede especificarla manualmente, la propiedad `ID` se suele generar automáticamente cuando se crea el objeto. Nunca debe cambiar el valor de `ID` después de haber empezado a crear un modelo. Todas las referencias a objetos de un modelo se basan en el valor de `ID`. Por tanto, si se cambia un valor de `ID` el modelo puede resultar dañado fácilmente.  
  
 Los objetos `DataSource` y `DataSourceView` tienen excepciones destacadas a las convenciones de nomenclatura. El valor de ID de un objeto `DataSource` se puede establecer en un solo punto (.), que no es único, como referencia a la base de datos actual. Una segunda excepción es `DataSourceView`, que se adhiere a las convenciones de nomenclatura definidas para los objetos `DataSet` en .NET Framework, donde `Name` se usa como identificador.  
  
 Las siguientes reglas se aplican a las propiedades `Name` e `ID`.  
  
-   Los nombres no distinguen mayúsculas de minúsculas. No puede tener un cubo denominado "sales" y otro denominado "Ventas" en la misma base de datos.  
  
-   No se permiten espacios iniciales o finales en el nombre de un objeto, aunque sí se pueden incluir espacios dentro de un nombre. Los espacios iniciales o finales se recortan implícitamente. Esto se aplica a los valores de `Name` e `ID` de un objeto.  
  
-   El número máximo de caracteres es 100.  
  
-   No hay ningún requisito especial para el primer carácter de un identificador. El primer carácter puede ser cualquier carácter válido.  
  
##  <a name="bkmk_reserved"></a> Palabras y caracteres reservados  
 Las palabras reservadas están en inglés y se aplican a los nombres de objeto, no a los títulos. Si usa accidentalmente una palabra reservada en un nombre de objeto, se producirá un error de validación. En los modelos multidimensionales y de minería de datos, las palabras reservadas que se describen a continuación no se pueden usar en ningún nombre de objeto en ningún momento.  
  
 En los modelos tabulares, donde la compatibilidad de la base de datos se establece en 1103, se han relajado las reglas de validación para ciertos objetos y no cumplen los requisitos de caracteres extendidos y las convenciones de nomenclatura de determinadas aplicaciones cliente. Las bases de datos que cumplen estos criterios están sujetas a reglas de validación menos estrictas. En este caso, es posible que un nombre de objeto incluya un carácter restringido y siga superando la validación.  
  
 **Palabras reservadas**  
  
-   AUX  
  
-   CLOCK$  
  
-   De COM1 a COM9 (COM1, COM2, COM3, etc.)  
  
-   CON  
  
-   De LPT1 a LPT9 (LPT1, LPT2, LPT3, etc.)  
  
-   NUL  
  
-   PRN  
  
-   NULL no se permite como carácter en ninguna cadena dentro del XML.  
  
 **Caracteres reservados**  
  
 La tabla siguiente muestra caracteres no válidos para objetos especificados.  
  
|Object|Caracteres no válidos|  
|------------|------------------------|  
|`Server`|Siga las convenciones de nomenclatura de servidores de Windows al asignar nombre a un objeto de servidor. Vea [Convenciones de nomenclatura (Windows)](/windows/desktop/DNS/naming-conventions) para obtener más detalles.|  
|`DataSource`|`: / \ * | ? " () [] {} <>`|  
|`Level` o `Attribute`|````. , ; ' ` : / \ * &| ? " & % $ ! + = [] {} \< >````|  
|`Dimension` o `Hierarchy`|````. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \<,>````|  
|Todos los demás objetos|````. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \< >````|  
  
 **Excepciones: Cuando se permiten caracteres reservados**  
  
 Como se ha indicado, los nombres de las bases de datos de una modalidad y un nivel de compatibilidad determinados pueden incluir caracteres reservados. Los nombres de objeto de atributo de dimensión, jerarquía, nivel, medida y KPI pueden incluir caracteres reservados para las bases de datos tabulares (1103 o superior) que permiten el uso de caracteres extendidos:  
  
|Modo de servidor y nivel de compatibilidad de base de datos|¿Se permiten caracteres reservados?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (todas las versiones)|Sin|  
|Tabular - 1050|Sin|  
|Tabular - 1100|Sin|  
|Tabular - 1130 y superior|Sí|  
  
 Las bases de datos pueden tener un ModelType predeterminado (default). Default es equivalente a multidimensional y por tanto no admite el uso de caracteres reservados en los nombres de columna.  
  
## <a name="see-also"></a>Vea también  
 [Palabras reservadas de MDX](/sql/mdx/mdx-reserved-words)   
 [Traducciones &#40;Analysis Services&#41;](../../../analysis-services/translations-analysis-services.md)   
 [Compatibilidad de análisis con XML for &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
