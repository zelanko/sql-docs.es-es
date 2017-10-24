---
title: Propiedad EditMode | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be4670f359212f1079044341285ec2b0aff6c559
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="editmode-property"></a>Propiedad EditMode
Indica el estado de edición del registro actual.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 ADO mantiene un búfer de edición asociado al registro actual. Esta propiedad indica si se realizaron cambios en este búfer, o si se ha creado un nuevo registro. Use la **EditMode** propiedad para determinar el estado de edición del registro actual. Puede probar cambios pendientes si un proceso de modificación se ha interrumpido y determinar si necesita usar el [actualización](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método.  
  
 En *modo de actualización inmediata* el **EditMode** propiedad se restablece a **adEditNone** después de una llamada correcta a la **actualizar** se llama al método . Cuando una llamada a [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) no eliminar correctamente el registro o registros en el origen de datos (por ejemplo, debido a infracciones de integridad referencial), el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) permanece en modo de edición (**EditMode** = **adEditInProgress**). Por lo tanto, **CancelUpdate** debe llamarse antes de trasladarse fuera del registro actual (por ejemplo con [mover](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), o [cerrar](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 En *modo de actualización por lotes* (en el que el proveedor almacena varios cambios en caché y los escribe en el origen de datos subyacente sólo cuando se llama a la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), el valor de la **EditMode ** propiedad se cambia cuando se realiza la primera operación y no se restablece mediante una llamada a la **actualización** método. Las operaciones posteriores no cambian el valor de la **EditMode** propiedad, incluso si se realizan operaciones diferentes. Por ejemplo, si es la primera operación Agregar un nuevo registro, y la segunda realiza cambios en una existente registrar, la propiedad de **EditMode** seguirá siendo **adEditAdd**. El **EditMode** propiedad no se restablece a **adEditNone** hasta después de la llamada a **UpdateBatch**. Para determinar qué operaciones se han realizado, establezca el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) para que sólo los registros con los cambios pendientes se verán y examine el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad de cada registro para determinar qué cambios se realizaron en los datos.  
  
> [!NOTE]
>  **EditMode** puede devolver un valor válido únicamente si hay un registro actual. **EditMode** devolverá un error si [BOF o EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es true, o si se ha eliminado el registro actual.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew (método) (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)

