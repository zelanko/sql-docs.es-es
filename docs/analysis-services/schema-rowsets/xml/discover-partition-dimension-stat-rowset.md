---
title: Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe43b694b8fdeb4128ae1ad2aa9dc137d2bc9d42
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37980428"
---
# <a name="discoverpartitiondimensionstat-rowset"></a>Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve estadísticas sobre la dimensión asociada a una partición.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_PARTITION_DIMENSION_STAT** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Obligatorio|El nombre de la base de datos.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre del cubo o modelo tabular.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre del grupo de medida.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre de la partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Nombre de la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||Nombre de un atributo en la dimensión.|  
|**ATTRIBUTE_INDEXED**|**DBTYPE_BOOL**||Cuando es true, indica que el atributo está indizado; de lo contrario, es false.|  
|**ATTRIBUTE_COUNT_MIN**|**DBTYPE_I8**||Recuento de atributo mínimo.|  
|**ATTRIBUTE_COUNT_MAX**|**DBTYPE_I8**||Recuento de atributo máximo.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
