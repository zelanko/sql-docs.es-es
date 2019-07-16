---
title: Propiedad EditMode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0ffc6fb258799b0ab0bb03e7acbd922f6a67d1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918983"
---
# <a name="editmode-property"></a>Propiedad EditMode
Indica el estado de edición del registro actual.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 ADO mantiene un búfer de edición asociado con el registro actual. Esta propiedad indica si se han realizado cambios a este búfer, o si se ha creado un nuevo registro. Use la **EditMode** propiedad para determinar el estado de edición del registro actual. Puede probar cambios pendientes si un proceso de edición se ha interrumpido y determinar si necesita usar el [actualización](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método.  
  
 En *modo de actualización inmediata* el **EditMode** propiedad se restablece a **adEditNone** después de una llamada correcta a la **actualizar** se llama al método . Cuando una llamada a [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) no eliminar correctamente el registro o registros del origen de datos (por ejemplo, debido a infracciones de integridad referencial), el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) permanece en modo de edición (**EditMode** = **adEditInProgress**). Por lo tanto, **CancelUpdate** debe llamarse antes de abandonar el registro actual (por ejemplo, con [mover](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), o [cerrar](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 En *modo de actualización por lotes* (en el que el proveedor almacena en caché varios cambios y los escribe en el origen de datos subyacente únicamente cuando se llama el [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), el valor de la **EditMode**  propiedad cambia cuando se realiza la primera operación y no se restablece mediante una llamada a la **actualización** método. Las operaciones posteriores no cambian el valor de la **EditMode** propiedad, incluso si se realizan operaciones diferentes. Por ejemplo, si la primera operación consiste en Agregar un nuevo registro y la segunda realiza cambios en una existente registra, la propiedad de **EditMode** seguirá siendo **adEditAdd**. El **EditMode** propiedad no se restablece a **adEditNone** hasta después de la llamada a **UpdateBatch**. Para determinar qué operaciones se han realizado, establezca el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) para que solo los registros con cambios pendientes se visible y examine el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad de cada registro para determinar qué cambios se realizaron en los datos.  
  
> [!NOTE]
>  **EditMode** puede devolver un valor válido solo si hay un registro actual. **EditMode** devolverá un error si [BOF o EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es true, o si se ha eliminado el registro actual.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew (método, ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Eliminar método (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
