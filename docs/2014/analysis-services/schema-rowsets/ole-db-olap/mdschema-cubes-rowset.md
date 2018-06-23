---
title: Conjunto de filas MDSCHEMA_CUBES | Documentos de Microsoft
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
- MDSCHEMA_CUBES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0044c9943b2f2819ea216c735f298b7e30de7a3a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199446"
---
# <a name="mdschemacubes-rowset"></a>Conjunto de filas MDSCHEMA_CUBES
  Describe la estructura de cubos dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_CUBES` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo o de la dimensión. Un símbolo del signo de dólar ($) prologa los nombres de la dimensión. **Nota:** sólo administradores de servidor y base de datos tienen permisos para ver cubos creados a partir de una dimensión.|  
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
 El `MDSCHEMA_CUBES` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Un mapa de bits con uno de estos valores válidos:<br /><br /> -CUBO 1<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`Base Cube_Name`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  