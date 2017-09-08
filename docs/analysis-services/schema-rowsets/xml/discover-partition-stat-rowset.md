---
title: Conjunto de filas DISCOVER_PARTITION_STAT | Documentos de Microsoft
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0863c2f263cc13ff9673063ab1f49535cd2407a3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discoverpartitionstat-rowset"></a>Conjunto de filas DISCOVER_PARTITION_STAT
  Devuelve estadísticas sobre agregaciones de una partición determinada.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_PARTITION_STAT** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Necesario|Nombre de la base de datos que contiene la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Necesario|Nombre del cubo o modelo tabular que contiene la partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Necesario|Nombre de un grupo de medidas en la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|**PARTICIÓN**|**DBTYPE_WSTR**|Necesario|El nombre de una partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
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
  
  
