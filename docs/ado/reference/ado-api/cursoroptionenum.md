---
title: CursorOptionEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CursorOptionEnum
helpviewer_keywords: CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c63c915bddd54bafecb20ac7d02595b6d18da84
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Especifica qué funcionalidad el [admite](../../../ado/reference/ado-api/supports-method.md) debe probar el método de.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Admite la [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método para agregar nuevos registros.|  
|**adApproxPosition**|0x4000|Admite la [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) y [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedades.|  
|**adBookmark**|0x2000|Admite la [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad para obtener acceso a registros específicos.|  
|**adDelete**|0x1000800|Admite la [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) método para eliminar registros.|  
|**adFind**|0x80000|Admite la [buscar](../../../ado/reference/ado-api/find-method-ado.md) método para buscar una fila en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera más registros o cambia la posición siguiente sin confirmar todos los cambios pendientes.|  
|**adIndex**|0x100000|Admite la [índice](../../../ado/reference/ado-api/index-property.md) propiedad que se va a denominar un índice.|  
|**adMovePrevious**|0x200|Admite la [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) y [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) métodos, y [mover](../../../ado/reference/ado-api/move-method-ado.md) o [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) métodos para mover el registro actual posición hacia atrás sin necesidad de marcadores.|  
|**adNotify**|0x40000|Indica que el proveedor de datos subyacente admite notificaciones (que determina si **Recordset** los eventos son compatibles).|  
|**adResync**|0x20000|Admite la [Resync](../../../ado/reference/ado-api/resync-method.md) método para actualizar el cursor con los datos que está visibles en la base de datos subyacente.|  
|**adSeek**|0x200000|Admite la [Seek](../../../ado/reference/ado-api/seek-method.md) método para buscar una fila en un **conjunto de registros**.|  
|**adUpdate**|0x1008000|Admite la [actualización](../../../ado/reference/ado-api/update-method.md) método para modificar datos existentes.|  
|**adUpdateBatch**|0x10000|Admite actualización por lotes ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) y [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos) para transmitir grupos de cambios en el proveedor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
