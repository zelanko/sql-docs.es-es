---
title: Conjunto de filas DISCOVER_PERFORMANCE_COUNTERS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 62b1e967-af67-4915-a305-727bffd61fe4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3f4f27d074ff01f02cc05c165e8acb1ea109198
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129245"
---
# <a name="discoverperformancecounters-rowset"></a>Conjunto de filas DISCOVER_PERFORMANCE_COUNTERS
  Devuelve el valor de uno o varios contadores de rendimiento. No admite los contadores que devuelven información acerca del uso a lo largo del tiempo (como las lecturas de disco por segundo y el porcentaje de uso de la CPU).  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_PERFORMANCE_COUNTERS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`PERF_COUNTER_NAME`|`DBTYPE_WSTR`|Obligatorio|El nombre del contador de rendimiento.|  
|`PERF_COUNTER_VALUE`|`DBTYPE_DOUBLE`||Valor del contador de rendimiento.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd2e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PerformanceCounters|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
