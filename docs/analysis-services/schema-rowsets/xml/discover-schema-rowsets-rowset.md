---
title: Conjunto de filas DISCOVER_SCHEMA_ROWSETS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2299df35b0e736a68e9d8416978dac73ca264974
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="discoverschemarowsets-rowset"></a>Conjunto de filas DISCOVER_SCHEMA_ROWSETS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve los nombres, restricciones, descripción y otra información para todos los valores de enumeración y cualquier valor de enumeración específico del proveedor adicional admitidos por el proveedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_SCHEMA_ROWSETS** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover**método devuelve el **DISCOVER_SCHEMA_ROWSETS** conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas DISCOVER_SCHEMA_ROWSETS contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**schemaName**|**DBTYPE_WSTR**||El nombre del esquema o solicitud. Esta solicitud devuelve valores de la enumeración *RequestTypes* .|  
|**SchemaGuid**|**DBTYPE_GUID**||GUID del esquema.|  
|**Restricciones**|**DBTYPE_HCHAPTER**||Una matriz de las restricciones admitidas por el proveedor.|  
|**Description**|**DBTYPE_WSTR**||Una descripción traducible del esquema.|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 Este conjunto de filas de esquema no está ordenado.  
  
 Para un proveedor que admite tres restricciones para el conjunto de filas de esquema DBSCHEMA_MEMBERS, la matriz **Restrictions** podría devolver el resultado siguiente. Los elementos en el resultado hacen referencia a los nombres de columna en el esquema.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_SCHEMA_ROWSETS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**schemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
