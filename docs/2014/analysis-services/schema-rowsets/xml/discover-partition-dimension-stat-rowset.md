---
title: Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT | Microsoft Docs
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
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f4dc209f985cafe804f81fa54fa68c56655d3e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310745"
---
# <a name="discoverpartitiondimensionstat-rowset"></a>Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT
  Devuelve estadísticas sobre la dimensión asociada a una partición.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_PARTITION_DIMENSION_STAT` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Obligatorio|El nombre de la base de datos.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre del cubo o modelo tabular.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre del grupo de medida.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre de la partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||Nombre de la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||Nombre de un atributo en la dimensión.|  
|`ATTRIBUTE_INDEXED`|`DBTYPE_BOOL`||Cuando es true, indica que el atributo está indizado; de lo contrario, es false.|  
|`ATTRIBUTE_COUNT_MIN`|`DBTYPE_I8`||Recuento de atributo mínimo.|  
|`ATTRIBUTE_COUNT_MAX`|`DBTYPE_I8`||Recuento de atributo máximo.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
