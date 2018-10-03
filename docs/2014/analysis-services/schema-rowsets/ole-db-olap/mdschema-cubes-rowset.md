---
title: Conjunto de filas MDSCHEMA_CUBES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_CUBES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7282ceaacc4778c205c27e6ef226855f94398be1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048405"
---
# <a name="mdschemacubes-rowset"></a>Conjunto de filas MDSCHEMA_CUBES
  Describe la estructura de cubos dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_CUBES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo o de la dimensión. Un símbolo del signo de dólar ($) prologa los nombres de la dimensión. **Nota:** solo servidor y los administradores de base de datos tienen permisos para ver cubos creados a partir de una dimensión.|  
|`CUBE_TYPE`|`DBTYPE_WSTR`||El tipo de cubo. Los valores válidos son:<br /><br /> -   `CUBE`<br />-   `DIMENSION`|  
|`CUBE_GUID`|`DBTYPE_GUID`||No compatible.|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||No compatible.|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||Muestra la última vez que se procesó el cubo.|  
|`SCHEMA_UPDATED_BY`|`DBTYPE_WSTR`||No compatible.|  
|`LAST_DATA_UPDATE`|`DBTYPE_DBTIMESTAMP`||Muestra la última vez que se procesó el cubo.|  
|`DATA_UPDATED_BY`|`DBTYPE_WSTR`||No compatible.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción del nodo fácil de comprender.|  
|`IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||Un valor booleano que siempre devuelve un valor verdadero.|  
|`IS_LINKABLE`|`DBTYPE_BOOL`||Un valor booleano que indica si un cubo se puede utilizar en un cubo vinculado.|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||Un valor booleano que indica si un cubo tiene permiso de escritura.|  
|`IS_SQL_ENABLED`|`DBTYPE_BOOL`||Un valor booleano que indica si se puede utilizar SQL en el cubo.|  
|`CUBE_CAPTION`|`DBTYPE_WSTR`||El título del cubo.|  
|`BASE_CUBE_NAME`|`DBTYPE_WSTR`||El nombre del cubo de origen si este cubo es un cubo de perspectiva.|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(Opcional) Conjunto de notas en formato XML.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_CUBES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Un mapa de bits con uno de estos valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`Base Cube_Name`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
