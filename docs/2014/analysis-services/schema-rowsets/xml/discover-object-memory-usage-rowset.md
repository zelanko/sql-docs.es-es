---
title: Conjunto de filas DISCOVER_OBJECT_MEMORY_USAGE | Documentos de Microsoft
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
helpviewer_keywords:
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ae1f26c1bc55c8aa080915a372710e4d59064979
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204694"
---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE, conjunto de filas
  Proporciona información sobre los recursos de memoria utilizados por los objetos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_OBJECT_MEMORY_USAGE` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`||Ruta de acceso al elemento primario del objeto actual.|  
|`OBJECT_ID`|`DBTYPE_WSTR`||Id. del objeto tal y como se define en el momento de su creación.|  
|`OBJECT_MEMORY_SHRINKABLE`|`DBTYPE_I8`||La cantidad total de memoria (bytes) usada por todos los objetos reducibles que tiene en propiedad directamente el objeto actual. El valor actual no incluye la memoria de los objetos que pertenecen a objetos con nombre que son propiedad del objeto actual.|  
|`OBJECT_MEMORY_NONSHRINKABLE`|`DBTYPE_I8`||La cantidad total de memoria (bytes) usada por todos los objetos que no son reducibles que tiene en propiedad directamente el objeto actual. El valor actual no incluye la memoria de los objetos que pertenecen a objetos con nombre que son propiedad del objeto actual.|  
|`OBJECT_VERSION`|`DBTYPE_I4`||Número de versión de metadatos del objeto. Este número cambia cada vez que se modifica el objeto.|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||Número de linaje de los datos del objeto. Este número se incrementa cada vez que se procesa el objeto.|  
|`OBJECT_TYPE_ID`|`DBTYPE_I4`||Reservada para uso interno.|  
|`OBJECT_TIME_CREATED`|`DBTYPE_DBTIMESTAMP`||Hora UTC del servidor en el momento en que se creó el objeto.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_OBJECT_MEMORY_USAGE` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`|Opcional.|  
|`OBJECT_ID`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  