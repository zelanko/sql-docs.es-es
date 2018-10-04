---
title: Conjunto de filas DBSCHEMA_TABLES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 66780a650e3187f3ec62831fd2badf331a1fca4d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153165"
---
# <a name="dbschematables-rowset"></a>Conjunto de filas DBSCHEMA_TABLES
  Identifica los grupos de medida y dimensiones expuestos como tablas dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DBSCHEMA_TABLES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|255|El nombre del catálogo al que pertenece este objeto.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|255|Nombre del cubo al que pertenece este objeto.|  
|`TABLE_NAME`|`DBTYPE_WSTR`|255|El nombre del objeto si `TABLE_TYPE` es `TABLE`.|  
|`TABLE_TYPE`|`DBTYPE_WSTR`||El tipo de la tabla.<br /><br /> `TABLE` indica que el objeto es un grupo de medida.<br /><br /> `SYSTEM TABLE` indica que el objeto es una dimensión.|  
|`TABLE_GUID`|`DBTYPE_GUID`||No compatible.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción legible del objeto.|  
|`TABLE_PROPID`|`DBTYPE_UI4`||No compatible.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||No compatible.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||Fecha de la última modificación del objeto.|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`||Tipo OLAP del objeto.<br /><br /> **MEASURE_GROUP** indica el objeto es un grupo de medida.<br /><br /> `CUBE_DIMENSION` indica que el objeto es una dimensión.|  
  
 El conjunto de filas se ordena en `TABLE_TYPE`, `TABLE_CATALOG`, `TABLE_SCHEMA` y `TABLE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DBSCHEMA_TABLES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_TYPE`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](ole-db-schema-rowsets.md)  
  
  
