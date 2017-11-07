---
title: Conjunto de filas DISCOVER_OBJECT_MEMORY_USAGE | Documentos de Microsoft
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
helpviewer_keywords:
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6bfd0d6517f974b60b3d35f25e5836bcd6a7c8e2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE, conjunto de filas
  Proporciona información sobre los recursos de memoria utilizados por los objetos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_OBJECT_MEMORY_USAGE** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||Ruta de acceso al elemento primario del objeto actual.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||Id. del objeto tal y como se define en el momento de su creación.|  
|**OBJECT_MEMORY_SHRINKABLE**|**DBTYPE_I8**||La cantidad total de memoria (bytes) usada por todos los objetos reducibles que tiene en propiedad directamente el objeto actual. El valor actual no incluye la memoria de los objetos que pertenecen a objetos con nombre que son propiedad del objeto actual.|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**DBTYPE_I8**||La cantidad total de memoria (bytes) usada por todos los objetos que no son reducibles que tiene en propiedad directamente el objeto actual. El valor actual no incluye la memoria de los objetos que pertenecen a objetos con nombre que son propiedad del objeto actual.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||Número de versión de metadatos del objeto. Este número cambia cada vez que se modifica el objeto.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||Número de linaje de los datos del objeto. Este número se incrementa cada vez que se procesa el objeto.|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||Reservada para uso interno.|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||Hora UTC del servidor en el momento en que se creó el objeto.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_OBJECT_MEMORY_USAGE** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|Opcional.|  
|**OBJECT_ID**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

