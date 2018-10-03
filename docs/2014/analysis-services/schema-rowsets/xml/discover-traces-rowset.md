---
title: Conjunto de filas DISCOVER_TRACES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26d40f737db108ea2a9f8a9cee05f3ee9503c73c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168247"
---
# <a name="discovertraces-rowset"></a>Conjunto de filas DISCOVER_TRACES
  Proporciona información acerca de los seguimientos que están activos en el servidor.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_TRACES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Descripción|  
|-----------------|--------------------|-----------------|  
|`TraceID`|`DBTYPE_WSTR`|Identificador de seguimiento.|  
|`TraceName`|`DBTYPE_WSTR`|Nombre de seguimiento.|  
|`LogFileName`|`DBTYPE_WSTR`|Nombre de archivo de registro de seguimiento.|  
|`LogFileSize`|`DBTYPE_I4`|Tamaño de archivo de registro de seguimiento.|  
|`LogFileRollover`|`DBTYPE_BOOL`|Cuando es true, indica que el archivo de registro debe sustituirse; de lo contrario, es false.|  
|`AutoRestart`|`DBTYPE_BOOL`|Cuando es true, indica que la opción de reinicio automático está habilitada; de lo contrario, es false.|  
|`CreationTime`|`DBTYPE_TIME`|Fecha y hora en que se creó el seguimiento.|  
|`StopTime`|`DBTYPE_TIME`|Hora de detención del seguimiento.|  
|`Type`|`PF_DBTYPE_WSTR`|Tipo de seguimiento.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_TRACES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|`DBTYPE_I4`|Opcional.|  
|`Type`|WSTR|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
