---
title: Conjunto de filas MDSCHEMA_MEASUREGROUPS | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_MEASUREGROUPS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d39a7ce85ec5c4781d69d5a0bcd2fb468dd701bc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasuregroups-rowset"></a>Conjunto de filas MDSCHEMA_MEASUREGROUPS
  Describe los grupos de medida dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **MDSCHEMA_MEASUREGROUPS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||El nombre del catálogo al que pertenece este grupo de medida. **NULL** si el proveedor no admite catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||No compatible.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**||Nombre del cubo al que pertenece este grupo de medida.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||Nombre del grupo de medida.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción legible del miembro.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||Un valor booleano que indica si el grupo de medida tiene permiso de escritura.<br /><br /> Devuelve **true** si el grupo de medida tiene permiso de escritura.|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||El título de presentación para el grupo de medida.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **MDSCHEMA_MEASUREGROUPS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

