---
title: Conjunto de filas DISCOVER_MEMORYUSAGE | Documentos de Microsoft
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
ms.assetid: e416ea61-9615-468c-a96f-bbf731f803b1
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dcbb314e1816757562f93290d95a3f9e345460b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discovermemoryusage-rowset"></a>Conjunto de filas DISCOVER_MEMORYUSAGE
  Devuelve las estadísticas de DISCOVER_MEMORYUSAGE para diversos objetos asignados por el servidor.  
  
> [!WARNING]  
>  Este conjunto de filas puede generar conjuntos de resultados muy grandes. Si los resultados no pueden mostrarse debido a que necesitan más memoria de presentación de la que permite SQL Server Management Studio, los resultados se escriben en un archivo temporal, en la siguiente ubicación predeterminada:  
>   
>  '\<unidad >: \Users\\< nombre de usuario\>\AppData\Local\Temp\\< fileID\>.xml'.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DISCOVER_MEMORYUSAGE** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Restricción|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MemoryID**|**DBTYPE_UI8**||Número que identifica la memoria.|  
|**MemoryName**|**DBTYPE_WSTR**||Nombre del objeto que posee la memoria.|  
|**SPID**|**DBTYPE_UI4**|Sí|Sesión que asignó memoria. Cero indica memoria no vinculada a una sesión específica.|  
|**CreationTime**|**DBTYPE_DBTIMESTAMP**||Es "la hora en que se creó el objeto" o "la hora en que se asignó la memoria".|  
|**BaseObjectType**|**DBTYPE_UI4**|Sí|Es un número que describe el tipo del objeto. Objetos con el mismo BaseObjectType tienen el mismo tipo.|  
|**MemoryUsed**|**DBTYPE_UI8**|Sí|Es el tamaño actual del objeto, que puede ser menor que la memoria asignada para que la use el objeto.|  
|**MemoryAllocated**|**DBTYPE_UI8**||Cantidad de memoria asignada para que la use el objeto, que se puede ser mayor que la cantidad de memoria que realmente usa el objeto.|  
|**MemoryAllocBase**|**DBTYPE_UI8**||Bytes asignados inicialmente para el propio objeto (excluidas las asignaciones adicionales para el contenido de objeto).|  
|**MemoryAllocFromAlloc**|**DBTYPE_UI8**||Memoria asignada para el contenido de este objeto.|  
|**Valor de ElementCount**|**DBTYPE_UI4**||Para un objeto contenedor, es el número de objetos que incluye dicho objeto.|  
|**Puede reducir**|**DBTYPE_BOOL**|Sí|Valor booleano que indica si la memoria se puede reducir (se puede desalojar debido a la presión de memoria). Si es true, la memoria se puede reducir; si es false, la memoria no se puede reducir.|  
|**ObjectParentPath**|**DBTYPE_WSTR**||Cadena que identifica la ruta de acceso completa de este objeto.|  
|**ObjectID**|**DBTYPE_WSTR**||Cadena que identifica el objeto. La ruta de acceso completa de este objeto se representa mediante la cadena: (ObjectParentPath + '.' + ObjectId).|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|A07CCD21-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|MemoryUsage|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

