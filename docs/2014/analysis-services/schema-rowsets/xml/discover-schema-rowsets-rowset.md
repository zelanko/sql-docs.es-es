---
title: Conjunto de filas DISCOVER_SCHEMA_ROWSETS | Microsoft Docs
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
- DISCOVER_SCHEMA_ROWSETS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa16f7ff677efd8e39367b9e618bdc95d778b405
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220245"
---
# <a name="discoverschemarowsets-rowset"></a>Conjunto de filas DISCOVER_SCHEMA_ROWSETS
  Devuelve los nombres, restricciones, descripción y otra información para todos los valores de enumeración y cualquier valor de enumeración específico del proveedor adicional admitidos por el proveedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_SCHEMA_ROWSETS` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_SCHEMA_ROWSETS` conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas DISCOVER_SCHEMA_ROWSETS contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`SchemaName`|`DBTYPE_WSTR`||El nombre del esquema o solicitud. Esta solicitud devuelve valores de la enumeración *RequestTypes* .|  
|`SchemaGuid`|`DBTYPE_GUID`||GUID del esquema.|  
|`Restrictions`|`DBTYPE_HCHAPTER`||Una matriz de las restricciones admitidas por el proveedor.|  
|`Description`|`DBTYPE_WSTR`||Una descripción traducible del esquema.|  
|`RestrictionsMask`|`DBTYPE_UI8`|||  
  
 Este conjunto de filas de esquema no está ordenado.  
  
 Para un proveedor que admite tres restricciones para el conjunto de filas de esquema DBSCHEMA_MEMBERS, la matriz `Restrictions` podría devolver el resultado siguiente. Los elementos en el resultado hacen referencia a los nombres de columna en el esquema.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_SCHEMA_ROWSETS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SchemaName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
