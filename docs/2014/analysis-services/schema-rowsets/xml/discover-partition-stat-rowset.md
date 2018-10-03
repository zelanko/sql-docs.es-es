---
title: Conjunto de filas DISCOVER_PARTITION_STAT | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 749756c55a305997d49ae165b86e71a1fc756be7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129755"
---
# <a name="discoverpartitionstat-rowset"></a>Conjunto de filas DISCOVER_PARTITION_STAT
  Devuelve estadísticas sobre agregaciones de una partición determinada.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_PARTITION_STAT` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre de la base de datos que contiene la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre del cubo o modelo tabular que contiene la partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre de un grupo de medidas en la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Obligatorio|El nombre de una partición.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`AGGREGATION_NAME`|`DBTYPE_WSTR`||Nombre de la agregación.|  
|`AGGREGATION_SIZE`|`DBTYPE_I8`||Tamaño de la agregación.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
