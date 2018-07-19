---
title: SELECT FROM &lt;modelo&gt;. DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29f730f0bdff985ffceb849c429e5d1b02f70d5f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992629"
---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM &lt;modelo&gt;. DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Un modelo de minería de datos se puede utilizar como una dimensión en un cubo OLAP, donde cada nodo del modelo se representa como un miembro de la dimensión. **SELECT FROM \<modelo >. Dimension_CONTENT** instrucción devuelve el contenido del modelo relativo a su uso como una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *lista de expresiones*  
 Lista delimitada por comas de identificadores de columna relacionados derivados del conjunto de filas de esquema CONTENT.  
  
 *model*  
 Identificador de modelo.  
  
 *expresión de condición*  
 Opcional. Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Notas  
 Los proveedores de algoritmos definen el contenido que se devuelve y cómo organizarlo. Por ejemplo, el proveedor podría limitar el número de nodos que se describen en el contenido de la dimensión.  
  
 En la siguiente tabla se muestran las columnas que se pueden consultar acerca del contenido de la dimensión y la función que realiza cada columna como dimensión de minería de datos.  
  
|Columna de conjunto de filas CONTENT|Función en la dimensión de minería de datos|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|Propiedad de miembro.|  
|NODE_NAME|Propiedad de miembro.|  
|NODE_UNIQUE_NAME|Atributo clave.|  
|NODE_TYPE|Propiedad de miembro.|  
|NODE_CAPTION|CaptionColumn para **clave** atributo.|  
|CHILDREN_CARDINALITY|Propiedad de miembro.|  
|PARENT_UNIQUE_NAME|RelatedAttribute para **clave** atributo (ParentAttribute en jerarquía de elementos primarios y secundarios).|  
|NODE_DESCRIPTION|Propiedad de miembro.|  
|NODE_RULE|Propiedad de miembro.|  
|MARGINAL_RULE|Propiedad de miembro.|  
|NODE_PROBABILITY|Propiedad de miembro.|  
|MARGINAL_PROBABILITY|Propiedad de miembro.|  
|NODE_SUPPORT|Propiedad de miembro.|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
 El ejemplo selecciona todas las columnas del contenido del modelo `[TM Decision Tree]` relacionadas con el uso del modelo como dimensión.  
  
### <a name="code"></a>código  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECCIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
