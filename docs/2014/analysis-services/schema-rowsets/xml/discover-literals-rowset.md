---
title: Conjunto de filas DISCOVER_LITERALS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_LITERALS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e218c03cd6d2f8dbf06501dd18a2c4c3e4977eca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063221"
---
# <a name="discoverliterals-rowset"></a>Conjunto de filas DISCOVER_LITERALS
  Devuelve información sobre los literales, incluidos los tipos de datos y valores, admitidos por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_LITERALS` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_LITERALS` conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_LITERALS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`LiteralName`|`DBTYPE_WSTR`||El nombre del literal descrito en la fila.<br /><br /> Por ejemplo, `DBLITERAL_LIKE_PERCENT`|  
|`LiteralValue`|`DBTYPE_WSTR`||Un valor literal real.<br /><br /> Por ejemplo, si `LiteralName` es `DBLITERAL_LIKE_PERCENT` y el carácter de porcentaje (`%`) coincide con ningún carácter o más en una cláusula LIKE, el valor de la columna `LiteralValue` es "`%`".|  
|`LiteralInvalidChars`|`DBTYPE_WSTR`||Caracteres que no son válidos en el literal.<br /><br /> Por ejemplo, si los nombres de tabla pueden contener algo distinto de un carácter numérico, esta cadena es "`0123456789`".|  
|`LiteralInvalidStartingChars`|`DBTYPE_WSTR`||Caracteres que no son válidos como el primer carácter del literal. Si el literal puede iniciar con cualquier carácter válido, éste es `null`.|  
|`LiteralMaxLength`|`DBTYPE_I4`||El número máximo de caracteres de un literal. Si no hay un valor máximo o se desconoce dicho valor, el valor es –1.|  
|`LiteralNameEnumValue`|`DBTYPE_I4`|||  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_LITERALS` conjunto de filas puede tener restricciones en las columnas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`LiteralName`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](xml-for-analysis-schema-rowsets.md)   
 [Conjunto de filas DISCOVER_KEYWORDS &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)  
  
  
