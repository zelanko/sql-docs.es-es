---
title: Conjunto de filas DISCOVER_TRACES | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7b3c8428b34a72f16986044db1652b9907384b07
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197702"
---
# <a name="discovertraces-rowset"></a>Conjunto de filas DISCOVER_TRACES
  Proporciona información acerca de los seguimientos que están activos en el servidor.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_TRACES` filas contiene las columnas siguientes.  
  
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
 El `DISCOVER_TRACES` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
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
  
  