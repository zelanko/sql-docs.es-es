---
title: RecordStatusEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 400d920692f8ee8d130caa5f3f98b46a11710a3d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="recordstatusenum"></a>RecordStatusEnum
Especifica la [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) de un registro con respecto a las actualizaciones por lotes y otras operaciones masivas.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Indica que no se guardó el registro porque se canceló la operación.|  
|**adRecCantRelease**|0x400|Indica que no se guardó el nuevo registro porque se ha bloqueado el registro existente.|  
|**adRecConcurrencyViolation**|0x800|Indica que no se guardó el registro porque se estaba utilizando simultaneidad optimista.|  
|**adRecDBDeleted**|0x40000|Indica que el registro se ha eliminado del origen de datos.|  
|**adRecDeleted**|0x4|Indica que el registro se ha eliminado.|  
|**adRecIntegrityViolation**|0x1000|Indica que no se guardó el registro porque el usuario infringió las restricciones de integridad.|  
|**adRecInvalid**|0x10|Indica que no se guardó el registro porque su marcador no es válido.|  
|**adRecMaxChangesExceeded**|0x2000|Indica que no se guardó el registro porque había demasiados cambios pendientes.|  
|**adRecModified**|0x2|Indica que se ha modificado el registro.|  
|**adRecMultipleChanges**|0x40|Indica que no se guardó el registro porque habría afectado a varios registros.|  
|**adRecNew**|0x1|Indica que el registro es nuevo.|  
|**adRecObjectOpen**|0x4000|Indica que no se guardó el registro debido a un conflicto con un objeto de almacenamiento abierto.|  
|**adRecOK**|0|Indica que el registro se actualizó correctamente.|  
|**adRecOutOfMemory**|0x8000|Indica que no se guardó el registro porque el equipo se ha quedado sin memoria.|  
|**adRecPendingChanges**|0x80|Indica que no se guardó el registro porque hace referencia a una inserción pendiente.|  
|**adRecPermissionDenied**|0x10000|Indica que no se guardó el registro porque el usuario no tiene permisos suficientes.|  
|**adRecSchemaViolation**|0x20000|Indica que no se guardó el registro porque infringe la estructura de la base de datos subyacente.|  
|**adRecUnmodified**|0x8|Indica que no se ha modificado el registro.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 AdoEnums.RecordStatus.  
  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
