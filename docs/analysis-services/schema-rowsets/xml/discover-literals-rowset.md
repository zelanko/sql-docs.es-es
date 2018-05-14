---
title: Conjunto de filas DISCOVER_LITERALS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ed865f22291b3e2e47c4934e455e0e75795d35cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="discoverliterals-rowset"></a>Conjunto de filas DISCOVER_LITERALS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve información sobre los literales, incluidos los tipos de datos y valores, admitidos por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_LITERALS** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover** método devuelve el **DISCOVER_LITERALS** conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DISCOVER_LITERALS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||El nombre del literal descrito en la fila.<br /><br /> Por ejemplo: **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||Un valor literal real.<br /><br /> Por ejemplo, si **LiteralName** es **DBLITERAL_LIKE_PERCENT** y el carácter de porcentaje (**%**) coincide con cero o más caracteres en una cláusula LIKE, el valor de la **LiteralValue** columna es "**%**".|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||Caracteres que no son válidos en el literal.<br /><br /> Por ejemplo, si los nombres de tabla pueden contener cualquier cosa que no sea un carácter numérico, esta cadena es "**0123456789**".|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||Caracteres que no son válidos como el primer carácter del literal. Si el literal puede iniciar con cualquier carácter válido, se trata de **null**.|  
|**LiteralMaxLength**|**DBTYPE_I4**||El número máximo de caracteres de un literal. Si no hay un valor máximo o se desconoce dicho valor, el valor es –1.|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **DISCOVER_LITERALS** se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [Conjunto de filas DISCOVER_KEYWORDS & #40; XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
