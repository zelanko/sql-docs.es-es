---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e91f82595c8e4f6fe07969960959a12464bf53a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708759"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
Especifica el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) de un registro con respecto a las actualizaciones por lotes y otras operaciones masivas.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Indica que no se guardó el registro porque se canceló la operación.|  
|**adRecCantRelease**|0x400|Indica que no se guardó el nuevo registro porque se ha bloqueado el registro existente.|  
|**adRecConcurrencyViolation**|0x800|Indica que no se guardó el registro porque la simultaneidad optimista estaba en uso.|  
|**adRecDBDeleted**|0x40000|Indica que el registro se ha eliminado del origen de datos.|  
|**adRecDeleted**|0x4|Indica que el registro se ha eliminado.|  
|**adRecIntegrityViolation**|0x1000|Indica que no se guardó el registro porque el usuario infringió las restricciones de integridad.|  
|**adRecInvalid**|0x10|Indica que no se guardó el registro porque su marcador no es válido.|  
|**adRecMaxChangesExceeded**|0x2000|Indica que no se guardó el registro porque había demasiados cambios pendientes.|  
|**adRecModified**|0x2|Indica que se modificó el registro.|  
|**adRecMultipleChanges**|0x40|Indica que no se guardó el registro porque habría afectado a varios registros.|  
|**adRecNew**|0x1|Indica que el registro es nuevo.|  
|**adRecObjectOpen**|0x4000|Indica que no se guardó el registro debido a un conflicto con un objeto de almacenamiento abierto.|  
|**adRecOK**|0|Indica que el registro se actualizó correctamente.|  
|**adRecOutOfMemory**|0x8000|Indica que no se guardó el registro porque el equipo se ha quedado sin memoria.|  
|**adRecPendingChanges**|0x80|Indica que no se guardó el registro porque hace referencia a una inserción pendiente.|  
|**adRecPermissionDenied**|0x10000|Indica que no se guardó el registro porque el usuario no tiene permisos suficientes.|  
|**adRecSchemaViolation**|0x20000|Indica que no se guardó el registro porque infringe la estructura de la base de datos subyacente.|  
|**adRecUnmodified**|0x8|Indica que no se modificó el registro.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
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
