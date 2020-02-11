---
title: CursorOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d5cc44950754c4b63e644d2d9210edcc94bd9ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933264"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Especifica qué funcionalidad debe probar el método [Supports](../../../ado/reference/ado-api/supports-method.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Admite el método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) para agregar nuevos registros.|  
|**adApproxPosition**|0x4000|Admite las propiedades [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) y [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) .|  
|**adBookmark**|0x2000|Admite la propiedad [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) para obtener acceso a registros específicos.|  
|**adDelete**|0x1000800|Admite el método [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) para eliminar registros.|  
|**Find**|0x80000|Admite el método [Find](../../../ado/reference/ado-api/find-method-ado.md) para buscar una fila en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera más registros o cambia la siguiente posición sin confirmar todos los cambios pendientes.|  
|**adIndex**|0x100000|Admite la propiedad de [Índice](../../../ado/reference/ado-api/index-property.md) para asignar un nombre a un índice.|  
|**adMovePrevious**|0x200|Admite los métodos [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) y [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) , y los métodos [Move](../../../ado/reference/ado-api/move-method-ado.md) o [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) para mover la posición del registro actual hacia atrás sin necesidad de marcadores.|  
|**adNotify**|0x40000|Indica que el proveedor de datos subyacente admite notificaciones (que determina si se admiten eventos de **conjunto de registros** ).|  
|**adResync**|0x20000|Admite el método [Resync](../../../ado/reference/ado-api/resync-method.md) para actualizar el cursor con los datos que están visibles en la base de datos subyacente.|  
|**adSeek**|0x200000|Admite el método [Seek](../../../ado/reference/ado-api/seek-method.md) para buscar una fila en un **conjunto de registros**.|  
|**adUpdate**|0x1008000|Admite el método [Update](../../../ado/reference/ado-api/update-method.md) para modificar los datos existentes.|  
|**adUpdateBatch**|0x10000|Admite la actualización por lotes (métodos[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) y [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) ) para transmitir grupos de cambios al proveedor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorOption. ADDNEW|  
|AdoEnums. CursorOption. APPROXPOSITION|  
|AdoEnums. CursorOption. BOOKMARK|  
|AdoEnums. CursorOption. DELETE|  
|AdoEnums. CursorOption. FIND|  
|AdoEnums. CursorOption. HOLDRECORDS|  
|AdoEnums. CursorOption. INDEX|  
|AdoEnums. CursorOption. MOVEPREVIOUS|  
|AdoEnums. CursorOption. NOTIFY|  
|AdoEnums. CursorOption. Resync|  
|AdoEnums. CursorOption. SEEK|  
|AdoEnums. CursorOption. UPDATE|  
|AdoEnums. CursorOption. UPDATEBATCH|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
