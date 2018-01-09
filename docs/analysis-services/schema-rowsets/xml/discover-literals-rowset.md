---
title: Conjunto de filas DISCOVER_LITERALS | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_LITERALS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae4dfbe2c5f7d9ce9281dd483b7544fb358dd1df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="discoverliterals-rowset"></a>Conjunto de filas DISCOVER_LITERALS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Devuelve información sobre los literales, incluidos los tipos de datos y valores, admitidos por el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML para el proveedor de Analysis (XMLA).  
  
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
 [Conjunto de filas DISCOVER_KEYWORDS &#40; XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
