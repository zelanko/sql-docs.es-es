---
title: Eliminar método (ADO Recordset) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b978e3d885e3ff06dda18859384f88eb4c564254
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919120"
---
# <a name="delete-method-ado-recordset"></a>Delete (método) (conjunto de registros ADO)
Elimina el registro actual o un grupo de registros.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Un [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina cuántos registros la **eliminar** afectará a método. El valor predeterminado es **adAffectCurrent**.  
  
> [!NOTE]
>  **adAffectAll** y **adAffectAllChapters** no son argumentos válidos para **eliminar**.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **eliminar** método marca el registro actual o un grupo de registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para su eliminación. Si el **Recordset** objeto no admite la eliminación de registros, se produce un error. Si está en modo de actualización inmediata, las eliminaciones se producen en la base de datos inmediatamente. Si un registro no puede eliminarse correctamente (debido a infracciones de la integridad de la base de datos, por ejemplo), el registro permanecerá en modo de edición después de llamar a [actualización](../../../ado/reference/ado-api/update-method.md). Esto significa que se debe cancelar la actualización con [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de abandonar el registro actual (por ejemplo, con [cerrar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), o [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Si está en modo de actualización por lotes, los registros se marcan para su eliminación de la memoria caché y la eliminación real se produce cuando se llama a la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Use la [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad para ver los registros eliminados.  
  
 Recuperar valores de campo desde el registro eliminado, genera un error. Después de eliminar el registro actual, el registro eliminado permanece actual hasta que se mueva a otro registro. Una vez que se mueva fuera del registro eliminado, ya no es accesible.  
  
 Si anida eliminaciones en una transacción, puede recuperar los registros eliminados con el [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Si está en modo de actualización por lotes, puede cancelar una eliminación pendiente o un grupo de eliminaciones pendientes con la [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Si se produce un error en el intento de eliminar registros debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ya se ha eliminado un registro), el proveedor devuelve advertencias a la [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección pero no detiene el programa ejecución. Se produce un error de tiempo de ejecución solo si hay conflictos en todos los registros solicitados.  
  
 Si el [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) se establece la propiedad dinámica y el **Recordset** es el resultado de ejecutar una operación JOIN en varias tablas, el **eliminar** método solo se eliminará las filas de la tabla mencionada en el [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Eliminar el ejemplo del método (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Eliminar método de ejemplo (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Eliminar el ejemplo del método (VC ++)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
