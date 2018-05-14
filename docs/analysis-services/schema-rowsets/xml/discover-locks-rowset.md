---
title: Conjunto de filas DISCOVER_LOCKS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7f0b52b875793df4074e9feb4e0cc1737224a901
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Proporciona información sobre los bloqueos pendientes actuales en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_LOCKS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LOCK_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||Hora del servidor UTC en el momento en que se solicitó el bloqueo.|  
|**LOCK_GRANT_TIME**|**DBTYPE_DBTIMESTAMP**||Hora del servidor UTC en el momento en que se concedió el bloqueo en el recurso.|  
|**LOCK_ID**|**DBTYPE_GUID**||Identificador único del bloqueo, como un GUID.|  
|**LOCK_OBJECT_ID**|**DBTYPE_WSTR**||Identificador único del objeto que se bloquea.|  
|**LOCK_STATUS**|**DBTYPE_I4**||Estado de bloqueo.<br /><br /> 0 significa "Esperando para bloquear el objeto".<br /><br /> 1 significa "Bloqueo concedido".|  
|**LOCK_TRANSACTION_ID**|**DBTYPE_GUID**||Identificador único de la transacción, como un GUID.|  
|**LOCK_TYPE**|**DBTYPE_I4**||Una máscara de bits de tipos de bloqueo; para obtener más información, consulte la sección Comentarios de este tema.|  
|**SPID**|**DBTYPE_I4**||Identificador de la sesión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_LOCKS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|Opcional.|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|Opcional.|  
|LOCK_STATUS|DBTYPE_I4|Opcional.|  
|LOCK_TYPE|DBTYPE_I4|Opcional.|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|Opcional.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="lock-types"></a>Tipos de bloqueo  
  
|Nombre de bloque|Value|Description|  
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
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
