---
title: Convenciones XML de ASSL | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d0411903c72aba9b0122beb4c0e46e9f172f4f4e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203061"
---
# <a name="assl-xml-conventions"></a>Convenciones XML de ASSL
  Analysis Services Scripting Language (ASSL) representa la jerarquía de objetos como un conjunto de tipos de elemento, cada uno de los cuales define los elementos secundarios que puede contener.  
  
 Para representar la jerarquía de objetos, ASSL utiliza las siguientes convenciones XML:  
  
-   Todos los objetos y las propiedades se representan como elementos, salvo los atributos XML estándar como "xml:lang".  
  
-   Nombres de elementos y valores de enumeración siguen la convención de nomenclatura de Microsoft .NET Framework de Pascal de mayúsculas y minúsculas sin caracteres de subrayado.  
  
-   Se conserva el uso de mayúsculas o minúsculas de todos los valores. Los valores de las enumeraciones también distinguen entre mayúsculas y minúsculas.  
  
 Además de esta lista de convenciones, Analysis Services sigue también ciertas convenciones con respecto a la cardinalidad, la herencia, el espacio en blanco, los tipos de datos y los valores predeterminados.  
  
## <a name="cardinality"></a>Cardinalidad  
 Cuando la cardinalidad de un elemento es mayor que 1, existe una colección de elementos XML que encapsula este elemento. El nombre de colección utiliza la forma plural de los elementos incluidos en la colección. Por ejemplo, el fragmento XML siguiente representa la colección `Dimensions` dentro de un elemento `Database`:  
  
 `<Database>`  
  
 `…`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 El orden en que aparecen los elementos no es significativo.  
  
## <a name="inheritance"></a>Herencia  
 La herencia se utiliza cuando existen objetos distintos con conjuntos de propiedades que se superponen pero son notablemente diferentes. Entre los ejemplos de tales objetos superpuestos pero distintos se encuentran los cubos virtuales, los cubos vinculados y los cubos normales. Para los objetos superpuestos pero distintos, Analysis Services utiliza el atributo `type` estándar del espacio de nombres de la instancia XML a fin de indicar la herencia. Por ejemplo, el fragmento XML siguiente muestra cómo el atributo `type` identifica si un elemento `Cube` hereda de un cubo normal o virtual:  
  
 `<Cubes>`  
  
 `<Cube xsi:type=”RegularCube”>`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type=”VirtualCube”>`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 Generalmente, la herencia no se utiliza cuando varios tipos tienen una propiedad con el mismo nombre. Por ejemplo, las propiedades `Name` e `ID` aparecen en muchos elementos, pero dichas propiedades no se han ascendido a un tipo abstracto.  
  
## <a name="whitespace"></a>Espacio en blanco  
 El espacio en blanco dentro de un valor de elemento se conserva. Sin embargo, el espacio en blanco inicial y final siempre se recorta. Por ejemplo, los elementos siguientes tienen el mismo texto pero cantidades distintas de espacio en blanco dentro de dicho texto, por lo tanto se tratan como si tuvieran valores distintos:  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 Sin embargo, los elementos siguientes solo varían respecto al espacio en blanco inicial y final y, por lo tanto, se tratan como si sus valores fueran equivalentes:  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>Tipos de datos  
 Analysis Services utiliza los siguientes tipos de datos del lenguaje de definición de esquema XML (XSD) estándar:  
  
 `Int`  
 Valor entero en el intervalo de -231 a 231 – 1.  
  
 `Long`  
 Valor entero en el intervalo de -263 a 263 – 1.  
  
 `String`  
 Valor de cadena que se ajusta a las reglas globales siguientes:  
  
-   Se eliminan los caracteres de control.  
  
-   Se recorta el espacio en blanco inicial y final.  
  
-   Se conserva el espacio en blanco interno.  
  
 Las propiedades `Name` e `ID` tienen limitaciones especiales respecto a los caracteres válidos en los elementos de cadena. Para obtener información adicional acerca de `Name` y `ID` convenciones, vea [ASSL y características de objetos](assl-objects-and-object-characteristics.md).  
  
 `DateTime`  
 Un `DateTime` estructura a partir de .NET Framework. Un valor `DateTime` no puede ser NULL. La fecha más antigua que admite el tipo de datos `DataTime` es el 1 de enero de 1601, disponible para los programadores como `DateTime.MinValue`. La fecha más antigua admitida indica que falta un valor `DateTime`.  
  
 `Boolean`  
 Enumeración con solo dos valores, como {true, false} o {0, 1}.  
  
## <a name="default-values"></a>Valores predeterminados  
 Analysis Services usa los valores predeterminados que se muestran en la tabla siguiente.  
  
|Tipo de datos de XML|Valor predeterminado|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|"" (cadena vacía)|  
|`Integer` o `Long`|0 (cero)|  
|`Timestamp`|12:00:00 A.M., 1/1/0001 (correspondiente a una las versiones de .NET Framework `System.DateTime` con 0 tics)|  
  
 Para un elemento que está presente pero vacío se interpreta que tiene un valor de cadena nula, no el valor predeterminado.  
  
### <a name="inherited-defaults"></a>Valores predeterminados heredados  
 Algunas propiedades especificadas en un objeto proporcionan valores predeterminados para la misma propiedad en los objetos secundarios o descendientes. Por ejemplo, `Cube.StorageMode` proporciona el valor predeterminado de `Partition.StorageMode`. Las reglas que Analysis Services aplica para los valores predeterminados heredados son las siguientes:  
  
-   Cuando la propiedad del objeto secundario tiene el valor NULL en XML, su valor predeterminado es el valor heredado. Sin embargo, si consulta el valor en el servidor, éste devuelve el valor NULL del elemento XML.  
  
-   No es posible determinar mediante programación si la propiedad de un objeto secundario se ha establecido directamente en el objeto secundario o se ha heredado.  
  
 Algunos elementos tienen valores predeterminados definidos que se aplican cuando falta el elemento. Por ejemplo, los elementos `Dimension` del fragmento XML siguiente son equivalentes aunque un elemento `Dimension` contiene un elemento `Visible`, pero no así el otro elemento `Dimension`.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Para obtener más información sobre los valores predeterminados heredados, consulte [ASSL y características de objetos](assl-objects-and-object-characteristics.md).  
  
  