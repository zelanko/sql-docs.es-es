---
title: Elemento NamingTemplate (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f6b25e36c78d8e03afd0c4a3ebb4ef9a96d2c9f8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040499"
---
# <a name="namingtemplate-element-assl"></a>Elemento NamingTemplate (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define cómo se denominan los niveles en una jerarquía de elementos primarios y secundarios construida a partir del [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **NamingTemplate** elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento de la **DimensionAttribute** elemento primario se establece en *primario*).  
  
 Cuando un atributo primario se utiliza para construir una jerarquía, las relaciones primario-secundario determinan los niveles de la jerarquía entre los miembros que se encuentran el atributo primario. Por consiguiente, a diferencia de otras dimensiones, los nombres de los niveles no se pueden deducir de los nombres de atributo utilizados para la jerarquía.  
  
 En lugar de ello, se usa una plantilla de nombres para generar los nombres de los niveles para las jerarquías primario-secundario. El elemento **NamingTemplate** , definido en el atributo primario, contiene una expresión de cadena utilizada para definir los nombres de los niveles. Hay dos maneras de definir una plantilla de nombres para un atributo primario. Puede diseñar un modelo de nombres, o especificar una lista de nombres.  
  
 Un modelo de nombres contiene un asterisco (`*`) como carácter marcador de posición de un contador que se incrementa y se inserta en el nombre de cada nivel nuevo y más profundo. Por ejemplo, si se utiliza `Level *` , se crean los nombres `Level 01`, `Level 02`, `Level 03`, etc., si no se define ningún nivel (Todos). Si un modelo de nombres no contiene el carácter marcador de posición, se utiliza primero como es y, a continuación, los nombres de los niveles subsiguientes se forman anexando un espacio y un número al final del modelo. Por ejemplo, si se usa `Level` , se crean los nombres de nivel `Level`, `Level 01`, `Level 02`, etc.  
  
 Para utilizar un conjunto concreto de nombres para los niveles, el valor del elemento **NamingTemplate** se establece en una lista de nombres de niveles delimitados por punto y coma. Cada nombre de la lista se utiliza para un nombre de nivel subsiguiente. Si el número de niveles supera el número de nombres de la lista, se usa el último nombre de la lista como plantilla para los nombres de niveles adicionales, con un espacio y un número ordinal anexados al último nombre como ya se ha descrito. Por ejemplo, si se usa `Division;Group;Unit` se crean los nombres de nivel `Division`, `Group`, `Unit`, `Unit 01`, `Unit 02`y así sucesivamente. Por otro lado, si se usa `Division;Group;Unit *` se crean los nombres de nivel `Division`, `Group`, `Unit 03`, `Unit 04`, etc.  
  
 Cada nombre de la lista se trata como una plantilla para garantizar la exclusividad de los nombres de nivel. Por ejemplo, si se usa `Manager;Team Lead;Manager;Team Lead;Worker *` se crean los nombres de nivel `Manager`, `Team Lead`, `Manager 01`, `Team Lead 01`, `Worker 05`, `Worker 06`.  
  
 Utilice dos asteriscos (*) para incluir el asterisco (\*) carácter en un nombre de nivel como parte de una plantilla de nombres.  
  
 El elemento que corresponde al elemento primario de **NamingTemplate** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento NamingTemplateTranslations &#40;ASSL&#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)   
 [Tipo de datos DimensionAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
