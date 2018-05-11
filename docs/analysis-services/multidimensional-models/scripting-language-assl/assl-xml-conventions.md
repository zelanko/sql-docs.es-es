---
title: Convenciones XML de ASSL | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4a1fee0f0ad96f17bc5c5c4c2d6fd1a61d524bc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="assl-xml-conventions"></a>Convenciones XML de ASSL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services Scripting Language (ASSL) representa la jerarquía de objetos como un conjunto de tipos de elemento, cada uno de los cuales define los elementos secundarios que puede contener.  
  
 Para representar la jerarquía de objetos, ASSL utiliza las siguientes convenciones XML:  
  
-   Todos los objetos y las propiedades se representan como elementos, salvo los atributos XML estándar como "xml:lang".  
  
-   Nombres de elementos y valores de enumeración siguen la convención de nomenclatura de Microsoft .NET Framework de Pascal de mayúsculas y minúsculas sin caracteres de subrayado.  
  
-   Se conserva el uso de mayúsculas o minúsculas de todos los valores. Los valores de las enumeraciones también distinguen entre mayúsculas y minúsculas.  
  
 Además de esta lista de convenciones, Analysis Services sigue también ciertas convenciones con respecto a la cardinalidad, la herencia, el espacio en blanco, los tipos de datos y los valores predeterminados.  
  
## <a name="cardinality"></a>Cardinalidad  
 Cuando la cardinalidad de un elemento es mayor que 1, existe una colección de elementos XML que encapsula este elemento. El nombre de colección utiliza la forma plural de los elementos incluidos en la colección. Por ejemplo, el fragmento XML siguiente representa la **dimensiones** colección dentro de un **base de datos** elemento:  
  
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
 La herencia se utiliza cuando existen objetos distintos con conjuntos de propiedades que se superponen pero son notablemente diferentes. Entre los ejemplos de tales objetos superpuestos pero distintos se encuentran los cubos virtuales, los cubos vinculados y los cubos normales. Para distintos los objetos superpuestos pero, Analysis Services utiliza la norma **tipo** atributo desde el Namespace de instancia XML para indicar la herencia. Por ejemplo, el fragmento XML siguiente muestra cómo el **tipo** atributo identifica si una **cubo** elemento hereda de un cubo normal o de un cubo virtual:  
  
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
  
 Generalmente, la herencia no se utiliza cuando varios tipos tienen una propiedad con el mismo nombre. Por ejemplo, el **nombre** y **identificador** propiedades aparecen en muchos elementos, pero estas propiedades no se han promocionado a un tipo abstracto.  
  
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
  
 **Int**  
 Valor entero en el intervalo de -231 a 231 – 1.  
  
 **Long**  
 Valor entero en el intervalo de -263 a 263 – 1.  
  
 **String**  
 Valor de cadena que se ajusta a las reglas globales siguientes:  
  
-   Se eliminan los caracteres de control.  
  
-   Se recorta el espacio en blanco inicial y final.  
  
-   Se conserva el espacio en blanco interno.  
  
 **Nombre** y **identificador** propiedades tienen limitaciones especiales respecto a los caracteres válidos en los elementos de cadena. Para obtener información adicional acerca de **nombre** y **identificador** convenciones, vea [ASSL y características de objetos](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 **DateTime**  
 A **DateTime** estructura a partir de .NET Framework. A **DateTime** valor no puede ser NULL. La fecha más antigua que admite la **DataTime** tipo de datos es el 1 de enero de 1601, que está disponible para los programadores como **DateTime.MinValue**. La fecha más antigua admitida indica que un **DateTime** falta el valor.  
  
 **Boolean**  
 Enumeración con solo dos valores, como {true, false} o {0, 1}.  
  
## <a name="default-values"></a>Valores predeterminados  
 Analysis Services usa los valores predeterminados que se muestran en la tabla siguiente.  
  
|Tipo de datos de XML|Valor predeterminado|  
|-------------------|-------------------|  
|**Boolean**|False|  
|**String**|"" (cadena vacía)|  
|**Entero** o **largo**|0 (cero)|  
|**marca de tiempo**|12:00:00 A.M., 1/1/0001 (correspondiente a una las versiones de .NET Framework **System.DateTime** con 0 tics)|  
  
 Para un elemento que está presente pero vacío se interpreta que tiene un valor de cadena nula, no el valor predeterminado.  
  
### <a name="inherited-defaults"></a>Valores predeterminados heredados  
 Algunas propiedades especificadas en un objeto proporcionan valores predeterminados para la misma propiedad en los objetos secundarios o descendientes. Por ejemplo, **Cube.StorageMode** proporciona el valor predeterminado de **Partition.StorageMode**. Las reglas que Analysis Services aplica para los valores predeterminados heredados son las siguientes:  
  
-   Cuando la propiedad del objeto secundario tiene el valor NULL en XML, su valor predeterminado es el valor heredado. Sin embargo, si consulta el valor en el servidor, éste devuelve el valor NULL del elemento XML.  
  
-   No es posible determinar mediante programación si la propiedad de un objeto secundario se ha establecido directamente en el objeto secundario o se ha heredado.  
  
 Algunos elementos tienen valores predeterminados definidos que se aplican cuando falta el elemento. Por ejemplo, el **dimensión** elementos en el siguiente fragmento XML son equivalentes aunque un **dimensión** elemento contiene un **Visible** elemento, pero los otros  **Dimensión** elemento no lo hace.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Para obtener más información sobre los valores predeterminados heredados, consulte [ASSL y características de objetos](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
  
