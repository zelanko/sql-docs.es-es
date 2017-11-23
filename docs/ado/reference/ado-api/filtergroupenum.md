---
title: FilterGroupEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: FilterGroupEnum
helpviewer_keywords: FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 080b0149fcfe0df39e1efbe44a87fe6243424468
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica el grupo de registros que se deben filtrar en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para ver solo los registros afectados por la última [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) llamar.|  
|**adFilterConflictingRecords**|5|Filtros para ver los registros que no se pudo la última actualización por lotes.|  
|**adFilterFetchedRecords**|3|Filtros para ver los registros en la memoria caché actual, es decir, los resultados de la última llamada para recuperar registros de la base de datos.|  
|**adFilterNone**|0|Quita el filtro actual y restaura todos los registros para su visualización.|  
|**adFilterPendingRecords**|1|Filtros para ver solo los registros que han cambiado pero no se han enviado todavía al servidor. Se aplica solo a modo de actualización por lotes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Filter](../../../ado/reference/ado-api/filter-property.md)
