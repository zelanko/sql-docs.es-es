---
title: Conjunto de filas DISCOVER_MEMORYUSAGE | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: abca3c8dc426e380b20c40db5a78d8300748aa0c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="discovermemoryusage-rowset"></a>Conjunto de filas DISCOVER_MEMORYUSAGE
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**valor de elementCount**|**DBTYPE_UI4**||Para un objeto contenedor, es el número de objetos que incluye dicho objeto.|  
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
  
  
