---
title: Conjunto de filas DISCOVER_KEYWORDS (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_KEYWORDS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0080afbf777cb06cf69c71e3d68b649f606d8658
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="discoverkeywords-rowset-xmla"></a>Conjunto de filas DISCOVER_KEYWORDS (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Devuelve información sobre las palabras clave reservadas por el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML para el proveedor de Analysis (XMLA).  
  
 Si se llama al método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) con el valor de enumeración **DISCOVER_KEYWORDS** en el elemento [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) , el método **Discover** devuelve el conjunto de filas **DISCOVER_KEYWORDS** .  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_KEYWORDS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Palabra clave**|**DBTYPE_WSTR**||Una lista de todas las palabras clave reservadas por un proveedor.<br /><br /> Ejemplo: **AND**|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_KEYWORDS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**Palabra clave**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [Conjunto de filas DISCOVER_LITERALS](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  
