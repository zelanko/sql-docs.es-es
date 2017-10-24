---
title: Conjunto de filas DISCOVER_PROPERTIES | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 374ca8fc9ce17f7da659a9718e8a7a531e8c3ca5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discoverproperties-rowset"></a>Conjunto de filas DISCOVER_PROPERTIES
  Devuelve una lista de información y valores sobre las propiedades estándar y específicas del proveedor admitidas por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para el origen de datos especificado. Las propiedades no compatibles no se muestran en el conjunto de resultados devuelto.  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_PROPERTIES** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover** método devuelve el **DISCOVER_PROPERTIES** conjunto de filas...  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_PROPERTIES** contiene las siguientes columnas.  
  
|Nombre de columna|Tipo|Longitud|Description|  
|-----------------|----------|------------|-----------------|  
|**PropertyName**|**DBTYPE_WSTR**||El nombre de la propiedad.|  
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
|**PropertyName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

