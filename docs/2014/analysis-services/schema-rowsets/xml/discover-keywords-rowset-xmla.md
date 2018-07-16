---
title: Conjunto de filas DISCOVER_KEYWORDS (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_KEYWORDS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a8be22c5132ed85ecb515ccadce20ecd593818a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241555"
---
# <a name="discoverkeywords-rowset-xmla"></a>Conjunto de filas DISCOVER_KEYWORDS (XMLA)
  Devuelve información sobre las palabras clave reservadas por el proveedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_KEYWORDS` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_KEYWORDS` conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_KEYWORDS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`Keyword`|`DBTYPE_WSTR`||Una lista de todas las palabras clave reservadas por un proveedor.<br /><br /> Ejemplo: `AND`|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_KEYWORDS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`Keyword`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](xml-for-analysis-schema-rowsets.md)   
 [Conjunto de filas DISCOVER_LITERALS](discover-literals-rowset.md)  
  
  
