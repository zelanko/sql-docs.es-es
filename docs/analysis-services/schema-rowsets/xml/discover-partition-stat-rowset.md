---
title: Conjunto de filas DISCOVER_PARTITION_STAT | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d2dd86a1ab15fbe9bcf11c6a4891fce22091fe58
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031436"
---
# <a name="discoverpartitionstat-rowset"></a>Conjunto de filas DISCOVER_PARTITION_STAT
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve estadísticas sobre agregaciones de una partición determinada.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_PARTITION_STAT** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre de la base de datos que contiene la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre del cubo o modelo tabular que contiene la partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Obligatorio|Nombre de un grupo de medidas en la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**PARTICIÓN**|**DBTYPE_WSTR**|Obligatorio|El nombre de una partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||Nombre de la agregación.|  
|**AGGREGATION_SIZE**|**DBTYPE_I8**||Tamaño de la agregación.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
