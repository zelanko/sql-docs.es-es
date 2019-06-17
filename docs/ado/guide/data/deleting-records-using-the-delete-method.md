---
title: Eliminación de registros mediante el método Delete | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b4798e2658bf23edaf7cd04fb819e26de2a55cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700825"
---
# <a name="deleting-records-using-the-delete-method"></a>Eliminar registros mediante el método Delete
Mediante el **eliminar** método marca el registro actual o un grupo de registros en un **Recordset** objeto para su eliminación. Si el **Recordset** objeto no permitir eliminación de registros, se produce un error. Si está en modo de actualización inmediata, las eliminaciones se producen en la base de datos inmediatamente. Si un registro no puede eliminarse correctamente (debido a infracciones de la integridad de la base de datos, por ejemplo), el registro permanecerá en modo de edición después de llamar a **Update.** Esto significa que se debe cancelar la actualización mediante [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de abandonar el registro actual (por ejemplo, mediante [cerrar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), o [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Si está en modo de actualización por lotes, los registros se marcan para su eliminación de la memoria caché y la eliminación real se produce cuando se llama a la **UpdateBatch** método. (Para ver los registros eliminados, establezca la **filtro** propiedad **adFilterAffectedRecords** después **eliminar** se denomina.)  
  
 Intentar recuperar los valores de campo del registro eliminado, genera un error. Después de eliminar el registro actual, el registro eliminado permanece actual hasta que se mueva a otro registro. Una vez que se mueva fuera del registro eliminado, ya no es accesible.  
  
 Si se anida eliminaciones en una transacción, puede recuperar los registros eliminados mediante el **RollbackTrans** método. Si está en modo de actualización por lotes, puede cancelar una eliminación pendiente o un grupo de eliminaciones pendientes mediante el **CancelBatch** método.  
  
 Si se produce un error en el intento de eliminar registros debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ya se ha eliminado un registro), el proveedor devuelve advertencias a la **errores** colección pero no detiene el programa ejecución. Se produce un error de tiempo de ejecución solo si hay conflictos en todos los registros solicitados.  
  
 Si el **tabla única** se establece la propiedad dinámica y la **Recordset** es el resultado de ejecutar una operación JOIN en varias tablas, el **eliminar** método eliminará solo filas desde la tabla mencionada en el **Unique Table** propiedad.  
  
 El **eliminar** método toma un argumento opcional que le permite especificar qué registros se ven afectados por la **eliminar** operación. Los únicos valores válidos para este argumento son cualquiera de los siguiente ADO **AffectEnum** constantes enumeradas:  
  
-   **adAffectCurrent** afecta a solo el registro actual.  
  
-   **adAffectGroup** afecta a solo los registros que cumplen actual **filtro** configuración de la propiedad. El **filtro** propiedad debe establecerse en un **FilterGroupEnum** valor o una matriz de **marcadores** para usar esta opción.  
  
 El código siguiente muestra un ejemplo de especificación **adAffectGroup** al llamar a la **eliminar** método. Este ejemplo agrega algunos registros en el ejemplo **Recordset** y actualiza la base de datos. A continuación, filtra el **Recordset** utilizando el **adFilterAffectedRecords** constante enumerada de filtro, que deja sólo los registros recién agregados visibles en el **conjunto de registros.** Por último, llama a la **eliminar** método y especifica que todos los registros que cumplen actual **filtro** se debe eliminar la configuración de la propiedad (los nuevos registros).  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
