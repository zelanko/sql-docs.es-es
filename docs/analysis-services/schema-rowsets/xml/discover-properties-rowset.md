---
title: Conjunto de filas DISCOVER_PROPERTIES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8752af7b67b69659ec3d9a348b4ec7c647f41c55
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="discoverproperties-rowset"></a>Conjunto de filas DISCOVER_PROPERTIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve una lista de información y valores sobre las propiedades estándar y específicas del proveedor admitidas por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para el origen de datos especificado. Las propiedades no compatibles no se muestran en el conjunto de resultados devuelto.  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_PROPERTIES** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover** método devuelve el **DISCOVER_PROPERTIES** conjunto de filas...  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_PROPERTIES** contiene las siguientes columnas.  
  
|Nombre de columna|Tipo|Longitud|Description|  
|-----------------|----------|------------|-----------------|  
|**propertyName**|**DBTYPE_WSTR**||El nombre de la propiedad.|  
|**PropertyDescription**|**DBTYPE_WSTR**||Una descripción del texto traducible de la propiedad. Puede devolver **NULL**.|  
|**PropertyType**|**DBTYPE_WSTR**||Tipo de datos XML de la propiedad.<br /><br /> Puede devolver **NULL**.|  
|**PropertyAccessType**|**DBTYPE_WSTR**||Acceso para la propiedad. El valor puede ser **Read**, **Write**o **ReadWrite**.|  
|**IsRequired**|**DBTYPE_BOOL**||Un booleano que indica si se necesita una propiedad.<br /><br /> True si se requiere una propiedad; false si no se requiere.<br /><br /> Puede devolver **NULL**.|  
|**Valor**|**DBTYPE_WSTR**||El valor actual de la propiedad.<br /><br /> Puede devolver **NULL**.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_PROPERTIES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**propertyName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
