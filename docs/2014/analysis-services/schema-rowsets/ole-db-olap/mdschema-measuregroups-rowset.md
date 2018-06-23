---
title: Conjunto de filas MDSCHEMA_MEASUREGROUPS | Documentos de Microsoft
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
- MDSCHEMA_MEASUREGROUPS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 046674dc7c579a99e3d9fd90a86c466001c270c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112103"
---
# <a name="mdschemameasuregroups-rowset"></a>Conjunto de filas MDSCHEMA_MEASUREGROUPS
  Describe los grupos de medida dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_MEASUREGROUPS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre del catálogo al que pertenece este grupo de medida. `NULL` si el proveedor no admite catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece este grupo de medida.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||Nombre del grupo de medida.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción legible del miembro.|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||Un valor booleano que indica si el grupo de medida tiene permiso de escritura.<br /><br /> Devuelve `true` si el grupo de medida tiene permiso de escritura.|  
|`MEASUREGROUP_CAPTION`|`DBTYPE_WSTR`||El título de presentación para el grupo de medida.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_MEASUREGROUPS` se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  