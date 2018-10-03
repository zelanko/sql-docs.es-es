---
title: Conjunto de filas MDSCHEMA_MEASUREGROUP_DIMENSIONS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be9e28aefd3170f8db73f21ae5f3f021be61c34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062681"
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>Conjunto de filas MDSCHEMA_MEASUREGROUP_DIMENSIONS
  Enumera las dimensiones de grupos de medida.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_MEASUREGROUP_DIMENSIONS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre del catálogo al que pertenece este grupo de medida. `NULL` si el proveedor no admite catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece este grupo de medida.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||Nombre del grupo de medida.|  
|`MEASUREGROUP_CARDINALITY`|`DBTYPE_WSTR`||El número de instancias que puede tener una medida en el grupo de medida para un único miembro de dimensión. Los valores posibles incluyen:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la dimensión.|  
|`DIMENSION_CARDINALITY`|`DBTYPE_WSTR`||El número de instancias que un miembro de dimensión puede tener para una instancia única de una medida de grupo de medida.<br /><br /> Los valores posibles incluyen:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||Un valor booleano que indica si las jerarquías en la dimensión están visibles.<br /><br /> Devuelve `TRUE` si una o más jerarquías en la dimensión están visibles; en caso contrario, `FALSE`.|  
|`DIMENSION_IS_FACT_DIMENSION`|`DBTYPE_BOOL`||Un valor booleano que indica si la dimensión es una dimensión de hechos.<br /><br /> Devuelve `TRUE` si la dimensión de una dimensión de hechos; en caso contrario, `FALSE`.|  
|`DIMENSION_PATH`|`DBTYPE_HCHAPTER`||Una lista de dimensiones para la dimensión de la referencia.|  
|`DIMENSION_GRANULARITY`|`DBTYPE_WSTR`||Nombre único de la jerarquía de granularidad.|  
  
 El conjunto de filas admite ordenando en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `MEASUREGROUP_NAME`, `DIMENSION_UNIQUE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_MEASUREGROUP_DIMENSIONS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 Visible<br />-2 no visible<br />-Restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
