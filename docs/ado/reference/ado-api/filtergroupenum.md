---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97add08a1d656e8c163600bb0ea8dda7fca264b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932647"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica el grupo de registros que se van a filtrar de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para ver solo los registros afectados por la llamada de última [eliminación](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [resincronización](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .|  
|**adFilterConflictingRecords**|5|Filtros para ver los registros que dieron error en la última actualización por lotes.|  
|**adFilterFetchedRecords**|3|Filtra para ver los registros en la caché actual; es decir, los resultados de la última llamada para recuperar los registros de la base de datos.|  
|**adFilterNone**|0|Quita el filtro actual y restaura todos los registros para su visualización.|  
|**adFilterPendingRecords**|1|Filtros para ver solo los registros que han cambiado pero que todavía no se han enviado al servidor. Aplicable solo para el modo de actualización por lotes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. FilterGroup. AFFECTEDRECORDS|  
|AdoEnums. FilterGroup. CONFLICTINGRECORDS|  
|AdoEnums. FilterGroup. FETCHEDRECORDS|  
|AdoEnums. FilterGroup. NONE|  
|AdoEnums. FilterGroup. PENDINGRECORDS|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Filter](../../../ado/reference/ado-api/filter-property.md)
