---
title: Conjunto de filas DISCOVER_PROPERTIES | Documentos de Microsoft
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
- DISCOVER_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: af566467345e29362a7b2fdd2c5bda04a35a6dd5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196550"
---
# <a name="discoverproperties-rowset"></a>Conjunto de filas DISCOVER_PROPERTIES
  Devuelve una lista de información y valores sobre las propiedades estándar y específicas del proveedor admitidas por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para el origen de datos especificado. Las propiedades no compatibles no se muestran en el conjunto de resultados devuelto.  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_PROPERTIES` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_PROPERTIES` conjunto de filas...  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_PROPERTIES` filas contiene las columnas siguientes.  
  
|Nombre de columna|Tipo|Longitud|Descripción|  
|-----------------|----------|------------|-----------------|  
|`PropertyName`|`DBTYPE_WSTR`||El nombre de la propiedad.|  
|`PropertyDescription`|`DBTYPE_WSTR`||Una descripción del texto traducible de la propiedad. Puede devolver `NULL`.|  
|`PropertyType`|`DBTYPE_WSTR`||Tipo de datos XML de la propiedad.<br /><br /> Puede devolver `NULL`.|  
|`PropertyAccessType`|`DBTYPE_WSTR`||Acceso para la propiedad. El valor puede ser `Read`, `Write` o `ReadWrite`.|  
|`IsRequired`|`DBTYPE_BOOL`||Un booleano que indica si se necesita una propiedad.<br /><br /> True si se requiere una propiedad; false si no se requiere.<br /><br /> Puede devolver `NULL`.|  
|`Value`|`DBTYPE_WSTR`||El valor actual de la propiedad.<br /><br /> Puede devolver `NULL`.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas `DISCOVER_PROPERTIES` puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`PropertyName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  