---
title: Conjunto de filas DISCOVER_TRACES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63bcb03d27abdacf675acd56c95a2dbd49adb362
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028726"
---
# <a name="discovertraces-rowset"></a>Conjunto de filas DISCOVER_TRACES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Proporciona información acerca de los seguimientos que están activos en el servidor.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_TRACES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**TraceID**|**DBTYPE_WSTR**|Identificador de seguimiento.|  
|**nombre de seguimiento**|**DBTYPE_WSTR**|Nombre de seguimiento.|  
|**LogFileName**|**DBTYPE_WSTR**|Nombre de archivo de registro de seguimiento.|  
|**LogFileSize**|**DBTYPE_I4**|Tamaño de archivo de registro de seguimiento.|  
|**LogFileRollover**|**DBTYPE_BOOL**|Cuando es true, indica que el archivo de registro debe sustituirse; de lo contrario, es false.|  
|**Reinicio automático**|**DBTYPE_BOOL**|Cuando es true, indica que la opción de reinicio automático está habilitada; de lo contrario, es false.|  
|**CreationTime**|**DBTYPE_TIME**|Fecha y hora en que se creó el seguimiento.|  
|**Hora de detención**|**DBTYPE_TIME**|Hora de detención del seguimiento.|  
|**Tipo**|**PF_DBTYPE_WSTR**|Tipo de seguimiento.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_TRACES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|**DBTYPE_I4**|Opcional.|  
|**Tipo**|WSTR|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
