---
title: Conjunto de filas DISCOVER_LOCKS | Documentos de Microsoft
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
- DISCOVER_LOCKS rowset
ms.assetid: dea48167-212c-40b7-a416-434042a1b697
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 41af6b328b9083151bd3ef51bfc7df1d2986c1cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107966"
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS, conjunto de filas
  Proporciona información sobre los bloqueos pendientes actuales en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_LOCKS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`LOCK_CREATION_TIME`|`DBTYPE_DBTIMESTAMP`||Hora del servidor UTC en el momento en que se solicitó el bloqueo.|  
|`LOCK_GRANT_TIME`|`DBTYPE_DBTIMESTAMP`||Hora del servidor UTC en el momento en que se concedió el bloqueo en el recurso.|  
|`LOCK_ID`|`DBTYPE_GUID`||Identificador único del bloqueo, como un GUID.|  
|`LOCK_OBJECT_ID`|`DBTYPE_WSTR`||Identificador único del objeto que se bloquea.|  
|`LOCK_STATUS`|`DBTYPE_I4`||Estado de bloqueo.<br /><br /> 0 significa "Esperando para bloquear el objeto".<br /><br /> 1 significa "Bloqueo concedido".|  
|`LOCK_TRANSACTION_ID`|`DBTYPE_GUID`||Identificador único de la transacción, como un GUID.|  
|`LOCK_TYPE`|`DBTYPE_I4`||Una máscara de bits de tipos de bloqueo; para obtener más información, consulte la sección Comentarios de este tema.|  
|`SPID`|`DBTYPE_I4`||Identificador de la sesión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_LOCKS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|Opcional.|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|Opcional.|  
|LOCK_STATUS|DBTYPE_I4|Opcional.|  
|LOCK_TYPE|DBTYPE_I4|Opcional.|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|Opcional.|  
  
## <a name="remarks"></a>Notas  
  
## <a name="lock-types"></a>Tipos de bloqueo  
  
|Nombre de bloque|Valor|Descripción|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|Ningún bloqueo.|  
|LOCK_SESSION_LOCK|0x0000001|Sesión inactiva; no interfiere con otros bloqueos.|  
|LOCK_READ|0x0000002|Bloqueo de lectura durante el proceso.|  
|LOCK_WRITE|0x0000004|Bloqueo de escritura durante el proceso.|  
|LOCK_COMMIT_READ|0x0000008|Confirmar bloqueo, compartido.|  
|LOCK_COMMIT_WRITE|0x0000010|Confirmar bloqueo, exclusivo.|  
|LOCK_COMMIT_ABORTABLE|0x0000020|Anular en el progreso de confirmación.|  
|LOCK_COMMIT_INPROGRESS|0x0000040|Confirmación en curso.|  
|LOCK_INVALID|0x0000080|Bloqueo no válido.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  